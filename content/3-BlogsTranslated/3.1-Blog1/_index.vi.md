---
title: "Lớp truy cập hợp nhất đa phương thức cho Poe của Quora sử dụng Amazon Bedrock"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---


Tác giả: Gilbert V. Lepadatu và Nick Huber | Ngày đăng: 16/09/2025 | Danh mục: [Amazon Bedrock](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/), [Customer Solutions](https://aws.amazon.com/blogs/machine-learning/category/post-types/customer-solutions/), [Foundation models](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/generative-ai/foundation-models/), [Generative AI](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/generative-ai/)

Các tổ chức đang tìm kiếm lợi thế cạnh tranh bằng cách triển khai và tích hợp nhanh chóng các mô hình trí tuệ nhân tạo sinh (Generative AI) thông qua kiến trúc Generative AI Gateway. Cách tiếp cận với giao diện hợp nhất này giúp đơn giản hóa việc truy cập vào nhiều mô hình nền tảng (foundation models – FMs), giải quyết một thách thức quan trọng: sự bùng nổ của các mô hình AI chuyên biệt, mỗi mô hình có khả năng, API và yêu cầu vận hành riêng biệt. Thay vì phải xây dựng và duy trì nhiều điểm tích hợp riêng lẻ cho từng mô hình, giải pháp thông minh là tạo ra một lớp trừu tượng (abstraction layer) để chuẩn hóa các khác biệt này đằng sau một API thống nhất và nhất quán.

Trung tâm Đổi mới Generative AI của AWS (AWS Generative AI Innovation Center) và Quora gần đây đã hợp tác để phát triển một giải pháp sáng tạo nhằm giải quyết chính thách thức này. Hai bên đã xây dựng một khung API bao bọc hợp nhất (unified wrapper API framework) giúp tăng tốc triển khai các mô hình nền tảng của Amazon Bedrock trên hệ thống Poe của Quora. Kiến trúc này mang lại khả năng “xây dựng một lần, triển khai nhiều mô hình” (build once, deploy multiple models), giúp rút ngắn đáng kể thời gian triển khai và công sức kỹ thuật, với mã cầu nối giao thức thực tế được thể hiện xuyên suốt trong mã nguồn.

Đối với các nhà lãnh đạo công nghệ và nhà phát triển đang làm việc với triển khai nhiều mô hình AI ở quy mô lớn, khung này minh chứng cho cách thiết kế trừu tượng thông minh và dịch giao thức (protocol translation) có thể tăng tốc chu kỳ đổi mới trong khi vẫn duy trì kiểm soát vận hành.

Trong bài viết này, chúng tôi sẽ trình bày chi tiết về cách AWS Generative AI Innovation Center và Quora hợp tác để xây dựng một khung API bao bọc hợp nhất, giúp tăng tốc đáng kể việc triển khai các mô hình nền tảng của Amazon Bedrock trên hệ thống Poe. Chúng tôi cũng sẽ phân tích kiến trúc kỹ thuật giúp kết nối giao thức ServerSentEvents theo hướng sự kiện của Poe với API REST của Amazon Bedrock, trình bày cách hệ thống cấu hình theo mẫu (template-based) giúp rút ngắn thời gian triển khai từ vài ngày xuống còn 15 phút, và chia sẻ các mẫu triển khai cho việc dịch giao thức, xử lý lỗi và hỗ trợ đa phương thức. Cách tiếp cận “xây dựng một lần, triển khai nhiều mô hình” này đã giúp Poe tích hợp hơn 30 mô hình Amazon Bedrock bao gồm văn bản, hình ảnh và video, đồng thời giảm tới 95% lượng thay đổi mã nguồn cần thiết.

### **Quora và Amazon Bedrock**

[Poe.com](http://poe.com/) là một hệ thống trí tuệ nhân tạo (AI) do Quora phát triển, cho phép người dùng và các nhà phát triển tương tác với một loạt các mô hình AI và trợ lý tiên tiến đến từ nhiều nhà cung cấp khác nhau. Hệ thống này hỗ trợ truy cập đa mô hình (multi-model access), cho phép người dùng trò chuyện song song với nhiều chatbot AI, phục vụ cho các tác vụ như hiểu ngôn ngữ tự nhiên, tạo nội dung, tạo hình ảnh, và nhiều ứng dụng khác.

Ảnh chụp màn hình dưới đây minh họa giao diện người dùng (UI) của Poe, nền tảng AI được Quora phát triển. Hình ảnh thể hiện thư viện phong phú các mô hình AI của Poe, được trình bày dưới dạng các “chatbot” riêng biệt mà người dùng có thể lựa chọn để tương tác.

![](/images/3-Blog/Blog1/1.png)

*Hình minh họa 1: Giao diện thư viện mô hình AI của Poe*

Ảnh chụp tiếp theo cung cấp cái nhìn về “Model Catalog” trong Amazon Bedrock, một dịch vụ được quản lý toàn phần (fully managed) của Amazon Web Services (AWS).  Danh mục này hoạt động như một trung tâm tập trung, giúp các nhà phát triển khám phá, đánh giá và truy cập các mô hình AI nền tảng (Foundation Models – FMs) tiên tiến đến từ nhiều nhà cung cấp khác nhau.

![](/images/3-Blog/Blog1/2.png)

*Hình minh họa 2: Giao diện danh mục mô hình (Model Catalog) trong Amazon Bedrock*

Ban đầu, việc tích hợp các mô hình nền tảng đa dạng có sẵn trong Amazon Bedrock đã đặt ra nhiều thách thức kỹ thuật lớn đối với nhóm phát triển của [Poe.com](http://Poe.com). Quá trình này đòi hỏi nguồn lực kỹ thuật đáng kể để thiết lập kết nối với từng mô hình riêng lẻ, đồng thời duy trì hiệu năng và độ tin cậy nhất quán giữa các mô hình. Tính dễ bảo trì (maintainability) cũng nhanh chóng trở thành một yếu tố then chốt, cùng với khả năng tích hợp nhanh các mô hình mới khi chúng được phát hành — hai yếu tố này làm tăng đáng kể độ phức tạp của quá trình tích hợp.

### **Thách thức kỹ thuật: Kết nối các hệ thống khác nhau**

Việc tích hợp giữa Poe và Amazon Bedrock đã đặt ra những thách thức kiến trúc cơ bản, đòi hỏi các giải pháp sáng tạo.  
 Hai hệ thống này được xây dựng dựa trên triết lý thiết kế và mô hình giao tiếp hoàn toàn khác nhau, tạo nên một khoảng cách kỹ thuật lớn mà API bao bọc (wrapper API) phải đóng vai trò cầu nối để giải quyết.

### **Sự khác biệt về kiến trúc**

Thách thức cốt lõi nằm ở sự khác biệt về kiến trúc giữa hai hệ thống. Việc hiểu rõ những khác biệt này là điều cần thiết để đánh giá mức độ phức tạp của giải pháp tích hợp. Poe vận hành dựa trên kiến trúc hiện đại, phản ứng thời gian thực (reactive architecture), sử dụng giao thức ServerSentEvents (SSE) thông qua thư viện FastAPI (fastapi\_poe). Kiến trúc này được tối ưu hóa cho các tương tác thời gian thực (stream-optimized), hoạt động theo mô hình phản hồi dựa trên sự kiện (event-driven response model), được thiết kế để hỗ trợ AI hội thoại liên tục (conversational AI). Amazon Bedrock, ngược lại, hoạt động như một dịch vụ đám mây doanh nghiệp (enterprise cloud service). Nó cung cấp giao diện REST với mẫu truy cập qua AWS SDK, yêu cầu chứng thực SigV4, có phạm vi mô hình giới hạn theo vùng AWS Region, và sử dụng mô hình yêu cầu–phản hồi (request–response) truyền thống, có hỗ trợ streaming. Sự không tương thích giữa các API này tạo ra nhiều thách thức kỹ thuật mà wrapper API của Poe phải xử lý, được tóm tắt trong bảng dưới đây.

#### Bảng: Các thách thức tích hợp giữa Poe và Amazon Bedrock

| Danh mục thách thức | Vấn đề kỹ thuật | Giao thức nguồn (Source) | Giao thức đích (Target) | Độ phức tạp tích hợp |
| ----- | ----- | ----- | ----- | ----- |
| **Dịch giao thức (Protocol Translation)** | Chuyển đổi giữa giao thức dựa trên WebSocket và API REST | WebSocket (hai chiều, duy trì kết nối) | REST (yêu cầu/đáp ứng, phi trạng thái) | Cao – yêu cầu xây dựng cầu nối giao thức |
| **Liên kết xác thực (Authentication Bridging)** | Kết nối xác thực JWT với cơ chế ký AWS SigV4 | Xác thực bằng token JWT | Xác thực AWS SigV4 | Trung bình – cần chuyển đổi thông tin xác thực |
| **Chuyển đổi định dạng phản hồi (Response Format Transformation)** | Chuyển đổi dữ liệu JSON sang định dạng yêu cầu | JSON tiêu chuẩn | Định dạng tùy chỉnh | Trung bình – cần ánh xạ cấu trúc dữ liệu |
| **Đồng bộ hóa luồng dữ liệu (Streaming Reconciliation)** | Chuyển đổi phản hồi phân mảnh (chunked responses) sang luồng SSE | Phản hồi HTTP dạng phân mảnh | Luồng ServerSentEvents | Cao – yêu cầu chuyển đổi luồng dữ liệu thời gian thực |
| **Chuẩn hóa tham số (Parameter Standardization)** | Tạo không gian tham số thống nhất cho nhiều mô hình khác nhau | Tham số riêng của từng mô hình | Giao diện tham số chuẩn hóa | Trung bình – cần chuẩn hóa cấu trúc tham số |

### **Tiến hóa của API và Converse API**

Vào tháng 5 năm 2024, Amazon Bedrock giới thiệu Converse API, mang lại nhiều lợi ích về chuẩn hóa, giúp đơn giản hóa đáng kể kiến trúc tích hợp. Các điểm nổi bật của Converse API bao gồm:

* Giao diện thống nhất cho nhiều nhà cung cấp mô hình khác nhau (như Anthropic, Meta, Mistral, v.v.).  
* Bộ nhớ hội thoại (conversation memory) với khả năng xử lý lịch sử trò chuyện một cách thống nhất.  
* Hỗ trợ cả chế độ streaming và non-streaming trong cùng một mô hình API duy nhất.  
* Hỗ trợ đa phương thức (multimodal) cho văn bản, hình ảnh và dữ liệu có cấu trúc.  
* Chuẩn hóa tham số (parameter normalization), giảm thiểu sự khác biệt trong cách triển khai của từng mô hình.  
* Tích hợp sẵn tính năng kiểm duyệt nội dung (built-in content moderation).

Giải pháp được trình bày trong bài viết này sử dụng Converse API khi phù hợp, đồng thời duy trì khả năng tương thích với các API riêng biệt của từng mô hình để khai thác các năng lực chuyên biệt. Cách tiếp cận lai (hybrid approach) này mang lại sự linh hoạt cao, đồng thời tận dụng tối đa lợi ích chuẩn hóa của Converse API.

### **Tổng quan giải pháp**

Framework API bao bọc (wrapper API framework) cung cấp một giao diện thống nhất (unified interface) giữa Poe và các mô hình trong Amazon Bedrock.  
 Nó hoạt động như một lớp dịch (translation layer) giúp chuẩn hóa các khác biệt giữa các mô hình và giao thức, đồng thời vẫn giữ nguyên các khả năng riêng biệt (unique capabilities) của từng mô hình AI.

Giải pháp được thiết kế dựa trên kiến trúc mô-đun (modular design), tách biệt rõ các chức năng độc lập (separation of concerns) và cho phép mở rộng linh hoạt (flexible scaling), như được minh họa trong sơ đồ dưới đây.

![](/images/3-Blog/Blog1/3.png)

*Hình minh họa 3: Kiến trúc tổng thể của framework Wrapper API giữa Poe và Amazon Bedrock*

Giải pháp wrapper API bao gồm nhiều thành phần chính, hoạt động phối hợp để mang lại trải nghiệm tích hợp liền mạch (seamless integration experience):

* #### **Client**: Đây là điểm đầu vào (entry point) nơi người dùng tương tác với các khả năng AI thông qua nhiều giao diện khác nhau (trình duyệt web, ứng dụng di động, API…).

* #### **Lớp Poe** bao gồm:

  * **Poe UI**: Chịu trách nhiệm về trải nghiệm người dùng (user experience), bao gồm việc tạo yêu cầu (request formation), quản lý tham số (parameter control), xử lý tải tệp (file uploads), và hiển thị phản hồi từ AI (response visualization).  
  * **Poe FastAPI**: Chuẩn hóa các tương tác của người dùng, đồng thời quản lý giao tiếp giữa client và các hệ thống nền tảng. Đây là lớp trung gian xử lý giao thức (protocol management layer), giúp duy trì tính nhất quán trong quá trình truyền tải dữ liệu và phản hồi.  
* **Bot Factory**: Đây là một cơ chế “nhà máy mô hình” (factory pattern), có nhiệm vụ tạo động (dynamically create) các bộ xử lý mô hình (model handlers) phù hợp với loại mô hình được yêu cầu — ví dụ: chat model (mô hình hội thoại), image model (mô hình tạo hình ảnh), video model (mô hình xử lý video).

Cấu trúc này cho phép hệ thống dễ dàng mở rộng (extensible) để hỗ trợ các loại mô hình mới hoặc biến thể khác nhau của mô hình hiện có trong tương lai. Dưới đây là một đoạn mã minh họa cách hoạt động của Bot Factory, thể hiện cách lựa chọn mô hình phù hợp dựa trên loại yêu cầu của người dùng:

    #From core/bot_factory.py - Actual implementation
    class BotFactory:
        """
        Factory for creating different types of bots.
        Handles bot creation based on the bot type and configuration.
        """
        @staticmethod
        def create_bot(bot_config: BotConfig) -> PoeBot:
            # Check if a custom bot class is specified
            if hasattr(bot_config, 'bot_class') and bot_config.bot_class:
                # Use the custom bot class directly
                bot = bot_config.bot_class(bot_config)
                
                # Explicitly ensure we're returning a PoeBot
                if not isinstance(bot, PoeBot):
                    raise TypeError(f"Custom bot class must return a PoeBot instance, got {type(bot)}")
                return bot

            # Determine bot type based on configuration
            if hasattr(bot_config, 'enable_video_generation') and bot_config.enable_video_generation:
                # Video generation bot
                if 'luma' in bot_config.bot_name:
                    from core.refactored_luma_bot import LumaVideoBot
                    return LumaVideoBot(bot_config)
                else:
                    from core.refactored_nova_reel_bot import NovaReelVideoBot
                    return NovaReelVideoBot(bot_config)
                    
            elif hasattr(bot_config, 'enable_image_generation') and bot_config.enable_image_generation:
                # Image generation bot
                if hasattr(bot_config, 'model_id') and "stability" in bot_config.model_id.lower():
                    # Stability AI image generation bot
                    from core.refactored_image_stability_ai import AmazonBedrockImageStabilityAIBot
                    return AmazonBedrockImageStabilityAIBot(bot_config)
                else:
                    # Other image generation bot (Titan, Canvas, etc.)
                    from core.refactored_image_bot_amazon import RefactoredAmazonImageGenerationBot
                    return RefactoredAmazonImageGenerationBot(bot_config)
                    
            else:
                # Check if this is a Claude 3.7 model
                if hasattr(bot_config, 'model_id') and "claude-3-7" in bot_config.model_id.lower():
                    return ClaudePlusBot(bot_config)
                else:
                    # Default to standard chat bot
                    return RefactoredAmazonBedrockPoeBot(bot_config)

* **Service manager:** Điều phối các dịch vụ cần thiết để xử lý yêu cầu một cách hiệu quả. Nó phối hợp giữa các dịch vụ chuyên biệt, bao gồm:  
  * **Token services** – Quản lý giới hạn token và theo dõi số lượng token sử dụng.  
  * **Streaming services** – Xử lý phản hồi thời gian thực.  
  * **Error services** – Chuẩn hóa và xử lý lỗi.  
  * **AWS service integration** – Quản lý các cuộc gọi API đến Amazon Bedrock.  
* **AWS services component** – Chuyển đổi phản hồi từ định dạng của Amazon Bedrock sang định dạng mà Poe mong đợi và ngược lại; xử lý các gói dữ liệu dạng streaming, hình ảnh và video.  
* **Amazon Bedrock layer** – Lớp dịch vụ mô hình nền tảng (FM) của Amazon, cung cấp khả năng xử lý AI thực tế và lưu trữ mô hình, bao gồm:  
  * **Model diversity** – Cung cấp quyền truy cập hơn 30 mô hình văn bản (như Amazon Titan, Amazon Nova, Claude của Anthropic, Llama của Meta, Mistral, v.v.), cũng như các mô hình hình ảnh và video.  
  * **API structure** – Hỗ trợ cả API riêng của từng mô hình và API hợp nhất Converse.  
  * **Authentication** – Yêu cầu xác thực AWS SigV4 để đảm bảo truy cập an toàn đến các điểm cuối của mô hình.  
  * **Response management** – Trả về kết quả mô hình kèm theo siêu dữ liệu và thống kê mức sử dụng được chuẩn hóa.

Luồng xử lý yêu cầu (Request processing flow) trong API hợp nhất này minh họa quá trình điều phối phức tạp khi kết nối giao thức ServerSentEvents (hướng sự kiện) của Poe với API REST của Amazon Bedrock, cho thấy nhiều dịch vụ chuyên biệt phối hợp nhịp nhàng để mang lại trải nghiệm người dùng liền mạch.

Quy trình bắt đầu khi client gửi yêu cầu thông qua giao diện Poe, sau đó yêu cầu được chuyển đến thành phần Bot Factory. Mẫu thiết kế *factory pattern* này tạo động (dynamically) trình xử lý mô hình phù hợp dựa trên loại mô hình được yêu cầu — có thể là chat, image, hoặc video generation. Tiếp đó, Service Manager sẽ điều phối các dịch vụ chuyên biệt cần thiết để xử lý yêu cầu một cách hiệu quả, bao gồm quản lý token, xử lý streaming và quản lý lỗi.

 Sơ đồ tuần tự dưới đây thể hiện toàn bộ luồng xử lý yêu cầu

![](/images/3-Blog/Blog1/4.png)

### **Mẫu cấu hình cho triển khai nhanh nhiều bot**

Điểm mạnh nhất của wrapper API nằm ở hệ thống mẫu cấu hình hợp nhất (unified configuration template system), cho phép triển khai và quản lý nhiều bot nhanh chóng với rất ít thay đổi trong mã nguồn. Cách tiếp cận này là trọng tâm trong thành công của giải pháp khi giúp rút ngắn đáng kể thời gian triển khai.

Hệ thống này sử dụng phương pháp cấu hình dựa trên mẫu (template-based configuration approach), trong đó kết hợp giữa các giá trị mặc định dùng chung (shared defaults) và các giá trị ghi đè riêng cho từng mô hình (model-specific overrides).

    # Bot configurations using the template pattern

    CHAT_BOTS = {
        'poe-nova-micro': BotConfig(
            # Identity
            bot_name='poe-nova-micro',
            model_id='amazon.nova-micro-v1:0',
            aws_region=aws_config['region'],
            poe_access_key='XXXXXXXXXXXXXXXXXXXXXX',

            # Model-specific parameters
            supports_system_messages=True,
            enable_image_comprehension=True,
            expand_text_attachments=True,
            streaming=True,
            max_tokens=1300,
            temperature=0.7,
            top_p=0.9,

            # Model-specific pricing
            enable_monetization=True,
            pricing_type="variable",
            input_token_cost_milli_cents=2,
            output_token_cost_milli_cents=4,
            image_analysis_cost_milli_cents=25,

            # Generate rate card with model-specific values
            custom_rate_card=create_rate_card(2, 4, 25),

            # Include common parameters
            **DEFAULT_CHAT_CONFIG
        ),

        'poe-mistral-pixtral': BotConfig(
            # Identity
            bot_name='poe-mistral-pixtral',
            model_id='us.mistral.pixtral-large-2502-v1:0',
            aws_region=aws_config['region'],
            poe_access_key='XXXXXXXXXXXXXXXXXXXXXX',

            # Model-specific parameters
            supports_system_messages=False,
            enable_image_comprehension=False,
            # ...
            # Include common parameters
            **DEFAULT_CHAT_CONFIG
        )
    }



Kiến trúc dựa trên cấu hình này mang lại nhiều lợi ích đáng kể, bao gồm:

* **Triển khai nhanh** – Việc thêm mô hình mới chỉ cần tạo một mục cấu hình mới thay vì phải viết lại mã tích hợp. Đây là yếu tố then chốt giúp cải thiện đáng kể thời gian triển khai.  
* **Quản lý tham số nhất quán** – Các tham số dùng chung được định nghĩa một lần trong DEFAULT\_CHAT\_CONFIG và kế thừa tự động bởi các bot, đảm bảo tính nhất quán và giảm trùng lặp cấu hình.  
* **Tùy chỉnh theo mô hình** – Mỗi mô hình có thể có thiết lập riêng biệt, nhưng vẫn hưởng lợi từ hạ tầng cấu hình chung.  
* **Linh hoạt trong vận hành**  – Các tham số có thể được điều chỉnh mà không cần thay đổi mã nguồn, giúp thử nghiệm và tối ưu hóa nhanh chóng.  
* **Quản lý thông tin xác thực tập trung** – Thông tin xác thực AWS được quản lý tập trung tại một nơi duy nhất, giúp tăng cường bảo mật và đơn giản hóa việc cập nhật.  
* **Triển khai theo vùng** – Các mô hình có thể được triển khai linh hoạt đến nhiều vùng AWS khác nhau, với các thiết lập vùng (Region settings) được kiểm soát trực tiếp tại cấp cấu hình.

Lớp BotConfig cung cấp một cách có cấu trúc (structured way) để định nghĩa cấu hình cho các bot, đồng thời hỗ trợ xác thực kiểu dữ liệu (type validation) trong quá trình triển khai:

    # From config/bot_config.py - Actual implementation (partial)
    class BotConfig(BaseModel):
        # Core Bot Identity
        bot_name: str = Field(..., description="Name of the bot")
        model_id: str = Field(..., description="Identifier for the AI model")

        # AWS Configuration
        aws_region: Optional[str] = Field(default="us-east-1", description="AWS region for deployment")
        aws_access_key: Optional[str] = Field(default=None, description="AWS access key")
        aws_secret_key: Optional[str] = Field(default=None, description="AWS secret key")
        aws_security_token: Optional[str] = None

        # Poe Configuration
        poe_access_key: str = Field(..., description="Poe access key")
        modal_app_name: str = Field(..., description="Modal app name")

        # Capability Flags
        allow_attachments: bool = Field(default=True, description="Whether to allow file attachments in Poe")
        supports_system_messages: bool = Field(default=False)
        enable_image_comprehension: bool = Field(default=False)
        expand_text_attachments: bool = Field(default=False)
        streaming: bool = Field(default=False)
        enable_image_generation: bool = Field(default=False)
        enable_video_generation: bool = Field(default=False)

        # Inference Configuration
        max_tokens: Optional[int] = Field(default=None, description="Maximum number of tokens to generate")
        temperature: Optional[float] = Field(default=None, description="Temperature for sampling")
        top_p: Optional[float] = Field(default=None, description="Top-p sampling parameter")
        optimize_latency: bool = Field(default=False, description="Enable latency optimization with performanceConfig")

        # Reasoning Configuration (Claude 3.7+)
        enable_reasoning: bool = Field(default=False, description="Enable Claude's reasoning capability")
        reasoning_budget: Optional[int] = Field(default=1024, description="Token budget for reasoning (1024-4000 recommended)")

        # Monetization Configuration
        enable_monetization: bool = Field(default=False, description="Enable variable pricing monetization")
        custom_rate_card: Optional[str] = Field(
            default=None,
            description="Custom rate card for variable pricing in markdown format"
        )
        input_token_cost_milli_cents: Optional[int] = Field(
            default=None,
            description="Cost per input token in thousandths of a cent"
        )
        output_token_cost_milli_cents: Optional[int] = Field(
            default=None,
            description="Cost per output token in thousandths of a cent"
        )
        image_analysis_cost_milli_cents: Optional[int] = Field(
            default=None,
            description="Cost per image analysis in thousandths of a cent"
        )



### **Khả năng đa phương thức nâng cao**

Một trong những điểm mạnh nhất của framework này là cách nó xử lý khả năng đa phương thức (multimodal) thông qua các cờ cấu hình đơn giản (simple configuration flags):

* **enable\_image\_comprehension** – Khi được đặt thành True đối với các mô hình chỉ xử lý văn bản (text-only) như Amazon Nova Micro, Poe tự sử dụng khả năng thị giác (vision capabilities) của mình để phân tích hình ảnh và chuyển đổi chúng thành mô tả văn bản, sau đó gửi các mô tả này đến mô hình của Amazon Bedrock.  
   Cơ chế này giúp ngay cả các mô hình chỉ-văn-bản cũng có thể phân loại hình ảnh mà không cần khả năng nhìn tích hợp sẵn.  
* **expand\_text\_attachments** – Khi được bật (True), Poe sẽ phân tích các tệp văn bản được tải lên và đưa nội dung của chúng vào hội thoại, cho phép mô hình làm việc trực tiếp với nội dung tài liệu mà không cần cơ chế xử lý tệp đặc biệt.  
* **supports\_system\_messages** – Tham số này kiểm soát việc mô hình có thể chấp nhận các thông điệp hệ thống (system prompts) hay không, giúp duy trì hành vi thống nhất giữa các mô hình có khả năng khác nhau.

Các cờ cấu hình này tạo nên một lớp trừu tượng mạnh mẽ (powerful abstraction layer), mang lại những lợi ích nổi bật sau:

* **Extends model capabilities** – Các mô hình chỉ-văn-bản có thể mô phỏng khả năng đa phương thức (pseudo-multimodal) nhờ bước xử lý trước (preprocessing) của Poe.  
* **Optimizes built-in features** – Các mô hình đa phương thức thực sự có thể tận dụng toàn bộ khả năng tích hợp sẵn để đạt hiệu quả tối ưu nhất.  
* **Simplifies integration** – Quá trình tích hợp trở nên đơn giản, chỉ cần bật hoặc tắt các tùy chọn cấu hình, không cần thay đổi mã nguồn.  
* **Maintains consistency** – Đảm bảo trải nghiệm người dùng nhất quán, bất kể khả năng gốc của mô hình là gì.

Tiếp theo, chúng ta sẽ đi sâu vào triển khai kỹ thuật của giải pháp (technical implementation) để hiểu chi tiết hơn về cách thức hoạt động.

### **Lớp dịch giao thức**

Khía cạnh thách thức kỹ thuật lớn nhất của giải pháp này nằm ở việc kết nối giữa các giao thức API của Poe và các giao diện mô hình đa dạng của Amazon Bedrock. Nhóm phát triển đã giải quyết vấn đề này bằng cách xây dựng một lớp dịch giao thức tinh vi (sophisticated protocol translation layer), cho phép các hệ thống hoạt động hài hòa dù được thiết kế theo những triết lý hoàn toàn khác nhau: 

    # From services/streaming_service.py - Actual implementation
    def _extract_content_from_event(self, event: Dict[str, Any]) -> Optional[str]:
        """Extract content from a streaming event based on model provider."""
        try:
            # Handle Anthropic Claude models
            if "message" in event:
                message = event.get("message", {})
                if "content" in message and isinstance(message["content"], list):
                    for content_item in message["content"]:
                        if content_item.get("type") == "text":
                            return content_item.get("text", "")
                elif "content" in message:
                    return str(message.get("content", ""))

            # Handle Amazon Titan models
            if "delta" in event:
                delta = event.get("delta", {})
                if "text" in delta:
                    return delta.get("text", "")

            # Handle other model formats
            if "chunk" in event:
                chunk_data = event.get("chunk", {})
                if "bytes" in chunk_data:
                    # Process binary data if present
                    try:
                        text = chunk_data["bytes"].decode("utf-8")
                        return json.loads(text).get("completion", "")
                    except Exception:
                        self.logger.warning("Failed to decode bytes in chunk")

            # No matching format found
            return None



Lớp dịch giao thức này (translation layer) xử lý những khác biệt tinh vi giữa các mô hình, đảm bảo rằng bất kể mô hình Amazon Bedrock nào được sử dụng, phản hồi gửi về cho Poe luôn thống nhất và tuân theo định dạng mà Poe mong đợi.

### **Xử lý và chuẩn hóa lỗi**

Một khía cạnh then chốt của việc triển khai là xử lý lỗi và chuẩn hóa lỗi toàn diện (comprehensive error handling and normalization). Thành phần ErrorService chịu trách nhiệm đảm bảo quá trình xử lý lỗi diễn ra nhất quán trên tất cả các mô hình khác nhau, giúp hệ thống duy trì tính ổn định và dễ bảo trì trong môi trường đa mô hình:

    # Simplified example of error handling (not actual code)
    class ErrorService:
        def normalize_Amazon_Bedrock_error(self, error: Exception) -> str:
            """Normalize Amazon Bedrock errors into a consistent format."""
            if isinstance(error, ClientError):
                if "ThrottlingException" in str(error):
                    return "The model is currently experiencing high demand. Please try again in a moment."
                elif "ValidationException" in str(error):
                    return "There was an issue with the request parameters. Please try again with different settings."
                elif "AccessDeniedException" in str(error):
                    return "Access to this model is restricted. Please check your permissions."
                else:
                    return f"An error occurred while communicating with the model: {str(error)}"
            elif isinstance(error, ConnectionError):
                return "Connection error. Please check your network and try again."
            else:
                return f"An unexpected error occurred: {str(error)}"

    Cách tiếp cận này đảm bảo rằng người dùng luôn nhận được các thông báo lỗi có ý nghĩa (meaningful error messages), bất kể mô hình nền tảng hay tình huống lỗi cụ thể đang xảy ra.

**Đếm và tối ưu hóa token**

Hệ thống triển khai cơ chế đếm và tối ưu hóa token tiên tiến (sophisticated token counting and optimization) nhằm tối đa hóa hiệu quả sử dụng các mô hình AI:

    # From services/streaming_service.py - Actual implementation (partial)
    # Calculate approximate JSON overhead
    user_message_tokens = 0
    for msg in conversation['messages']:
        for content_block in msg.get('content', []):
            if 'text' in content_block:
                # Simple word-based estimation of actual text content
                user_message_tokens += len(content_block['text'].split())

    # Estimate JSON structure overhead (difference between total and content)
    json_overhead = int((input_tokens - system_tokens) - user_message_tokens)

    # Ensure we're working with integers for calculations
    input_tokens_for_pct = int(input_tokens)
    system_tokens_for_pct = int(system_tokens)
    json_overhead_for_pct = int(json_overhead)

    # Calculate percentage with float arithmetic and proper integer division
    json_overhead_percent = (float(json_overhead_for_pct) / max(1, input_tokens_for_pct - system_tokens_for_pct)) * 100
    ...



Việc theo dõi chi tiết token này cho phép ước tính chi phí và tối ưu hóa chính xác, giúp sử dụng tài nguyên mô hình hiệu quả hơn.

### **Xác thực và bảo mật AWS**

Thành phần AwsClientService chịu trách nhiệm xác thực và bảo mật cho các lệnh gọi API của Amazon Bedrock. Triển khai này đảm bảo xác thực an toàn với các dịch vụ AWS, đồng thời xử lý lỗi và quản lý kết nối một cách đúng chuẩn và nhất quán.

### **Phân tích so sánh**

Việc triển khai wrapper API đã cải thiện đáng kể hiệu suất và khả năng triển khai các mô hình Amazon Bedrock trên Poe, như được thể hiện trong bảng sau:

| Feature | Before (Direct API) | After (Wrapper API) |
| ----- | ----- | ----- |
| **Deployment Time** | Days per model | Minutes per model |
| **Developer Focus** | Configuration and plumbing | Innovation and features |
| **Model Diversity** | Limited by integration capacity | Extensive (across Amazon Bedrock models) |
| **Maintenance Overhead** | High (separate code for each model) | Low (configuration-based) |
| **Error Handling** | Custom per model | Standardized across models |
| **Cost Tracking** | Complex (multiple integrations) | Simplified (centralized) |
| **Multimodal Support** | Fragmented | Unified |
| **Security** | Varied implementations | Consistent best practices |

Bảng so sánh này làm nổi bật những cải tiến đáng kể đạt được thông qua cách tiếp cận wrapper API, minh chứng cho giá trị của việc đầu tư vào một lớp trừu tượng mạnh mẽ (robust abstraction layer).

### **Hiệu suất và tác động kinh doanh**

### Framework wrapper API đã mang lại tác động kinh doanh rõ rệt và có thể đo lường được trên nhiều khía cạnh, bao gồm tăng tính đa dạng mô hình, nâng cao hiệu quả triển khai, và cải thiện năng suất của nhà phát triển.

Poe hiện có thể mở rộng nhanh chóng danh mục mô hình của mình, tích hợp hàng chục mô hình Amazon Bedrock trên các loại dữ liệu văn bản, hình ảnh và video. Việc mở rộng này diễn ra trong vài tuần thay vì vài tháng như trước đây.

Bảng dưới đây tóm tắt các chỉ số hiệu quả triển khai (deployment efficiency metrics):

| Chỉ số | Trước | Sau | Cải thiện |
| ----- | ----- | ----- | ----- |
| **Triển khai mô hình mới** | 2–3 ngày | 15 phút | Nhanh hơn 96 lần |
| **Số dòng mã cần thay đổi** | Hơn 500 dòng | 20–30 dòng | Giảm 95% |
| **Thời gian thử nghiệm** | 8–12 giờ | 30–60 phút | Giảm 87% |
| **Các bước triển khai** | 10–15 bước | 3–5 bước | Giảm 75% |

Các chỉ số này được đo lường thông qua so sánh trực tiếp số giờ kỹ sư thực hiện trước và sau khi triển khai, theo dõi các lần triển khai thực tế của các mô hình mới.

Nhóm kỹ sư cũng ghi nhận sự thay đổi rõ rệt trong phân bổ thời gian công việc, chuyển trọng tâm từ tích hợp API sang phát triển tính năng, như thể hiện trong bảng dưới đây:

| Hoạt động | Trước (% thời gian) | Sau (% thời gian) | Thay đổi |
| ----- | ----- | ----- | ----- |
| Tích hợp API | 65% | 15% | \-50% |
| Phát triển tính năng | 20% | 60% | \+40% |
| Thử nghiệm | 10% | 15% | \+5% |
| Tài liệu | 5% | 10% | \+5% |

### **Cân nhắc về khả năng mở rộng và hiệu năng**

### Wrapper API được thiết kế để xử lý các khối lượng công việc lớn trong môi trường sản xuất (high-volume production workloads) với khả năng mở rộng mạnh mẽ (robust scaling capabilities).

**Connection pooling**

Để xử lý hiệu quả nhiều yêu cầu đồng thời (multiple concurrent requests), hệ thống wrapper triển khai cơ chế gom kết nối (connection pooling) bằng cách sử dụng thư viện aiobotocore. Cơ chế này cho phép hệ thống duy trì một nhóm (pool) các kết nối đến Amazon Bedrock, giúp giảm chi phí xử lý khi phải thiết lập kết nối mới cho từng yêu cầu riêng lẻ: 

    # From services/aws_service.py - Connection management
    async def setup_client(self) -> None:
        """Initialize AWS client with proper configuration."""
        async with self._client_lock:
            try:
                # Always clean up existing clients first to avoid stale connections
                if self.Amazon_Bedrock_client:
                    await self.cleanup()

                # Increase timeout for image generation
                config = Config(
                    read_timeout=300,  # 5 minutes timeout
                    retries={'max_attempts': 3, 'mode': 'adaptive'},
                    connect_timeout=30  # 30 second connection timeout
                )

                # Create the Amazon Bedrock client with proper error handling
                self.Amazon_Bedrock_client = await self.session.create_client(
                    service_name="Amazon_Bedrock-runtime",
                    region_name=self.bot_config.aws_region,
                    aws_access_key_id=self.bot_config.aws_access_key,
                    aws_secret_access_key=self.bot_config.aws_secret_key,
                    aws_session_token=self.bot_config.aws_security_token,
                    config=config
                ).__aenter__()
            except Exception as e:
                self.Amazon_Bedrock_client = None
                raise

### **Xử lý bất đồng bộ**

Toàn bộ framework được thiết kế theo cơ chế xử lý bất đồng bộ (asynchronous processing) nhằm xử lý hiệu quả nhiều yêu cầu đồng thời (concurrent requests):

    # From core/refactored_chat_bot.py - Asynchronous request handling
    async def get_response(self, query: QueryRequest) -> AsyncIterable[PartialResponse]:
        try:
            # Ensure AWS client is set up
            await aws_service.setup_client()

            # Validate and format the conversation
            conversation = await conversation_service.validate_conversation(query)

            # Process the request with streaming
            if self.bot_config.streaming:
                async for chunk in streaming_service.stream_Amazon_Bedrock_response(conversation, request_id):
                    yield chunk
            else:
                # Non-streaming mode
                response_text, input_tokens, output_tokens = await streaming_service.non_stream_Amazon_Bedrock_response(conversation, request_id)
                if response_text:
                    yield PartialResponse(text=response_text)
                else:
                    yield PartialResponse(text=self.bot_config.fallback_response)
                # Send done event for non-streaming mode
                yield self.done_event()

        except Exception as e:
            # Error handling
            error_message = error_service.log_error(e, request_id, "Error during request processing")
            yield PartialResponse(text=error_message)
            yield self.done_event()

### **Khôi phục lỗi và logic thử lại**

### Hệ thống triển khai cơ chế khôi phục lỗi (error recovery) và logic thử lại thông minh (retry logic) nhằm xử lý các sự cố tạm thời (transient issues) một cách hiệu quả và tự động:

    # From services/streaming_service.py - Retry logic
    max_retries = 3
    base_delay = 1  # Start with 1 second delay

    for attempt in range(max_retries):
        try:
            if not self.aws_service.Amazon_Bedrock_client:
                yield PartialResponse(text="Error: Amazon Bedrock client is not initialized")
                break

            response = await self.aws_service.Amazon_Bedrock_client.converse_stream(**stream_config)
            # Process response...
            break  # Success, exit retry loop

        except ClientError as e:
            if "ThrottlingException" in str(e):
                if attempt < max_retries - 1:
                    delay = base_delay * (2 ** attempt)  # Exponential backoff
                    await asyncio.sleep(delay)
                    continue
            error_message = f"Amazon Bedrock API Error: {str(e)}"
            yield PartialResponse(text=f"Error: {error_message}")
            break



### **Chỉ số hiệu năng**

### Hệ thống thu thập các chỉ số hiệu năng chi tiết (detailed performance metrics) nhằm xác định các điểm nghẽn (bottlenecks) và tối ưu hóa hiệu suất hoạt động tổng thể (optimize performance):

    # From services/streaming_service.py - Performance metrics
    # Log token usage and latency
    latency = time.perf_counter() - start_time

    self.logger.info(
    f"[{request_id}] Streaming Response Metrics:\n"
    f" Time to First Token: {first_token_time:.4f} seconds\n"
    f" Input Tokens: {input_tokens} (includes system prompt)\n"
    f" Input Tokens for Billing: {input_tokens - system_tokens} (excludes system prompt)\n"
    f" Output Tokens: {output_tokens}\n"
    f" Total Tokens: {total_tokens}\n"
    f" Amazon Bedrock Latency: {latency:.4f} seconds\n"
    f" Latency Optimization: {'enabled' if hasattr(self.bot_config, 'optimize_latency') and self.bot_config.optimize_latency else 'disabled'}"
    )


### **Các yếu tố bảo mật**

### Bảo mật là một khía cạnh then chốt trong việc triển khai wrapper API, với nhiều tính năng quan trọng được thiết kế để đảm bảo hoạt động an toàn của hệ thống.

### **Xác thực JWT kết hợp chữ ký AWS SigV4**

Hệ thống tích hợp xác thực JWT cho các yêu cầu từ Poe, đồng thời sử dụng AWS SigV4 signing để bảo mật các lệnh gọi Amazon Bedrock API, bao gồm:

* JWT validation – Đảm bảo rằng chỉ những yêu cầu được ủy quyền từ Poe mới có thể truy cập wrapper API.  
* SigV4 signing – Đảm bảo wrapper API có thể xác thực an toàn với Amazon Bedrock.  
* Credential management – Thông tin xác thực AWS được quản lý an toàn và không bao giờ lộ ra phía client.

### **Quản lý bí mật**

Hệ thống được tích hợp với [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/) để lưu trữ và truy xuất an toàn các thông tin nhạy cảm (sensitive credentials):

    # From services/aws_service.py - Secrets management
    @staticmethod
    def get_secret(secret_name: str, region_name: str = "us-east-1") -> Dict[str, Any]:
        """
        Retrieve a secret from AWS Secrets Manager.

        Args:
            secret_name: Name of the secret to retrieve
            region_name: AWS region where the secret is stored

        Returns:
            Dict[str, Any]: The secret value as a dictionary
        """
        # Create a Secrets Manager client
        session = boto3.session.Session()
        client = session.client(
            service_name='secretsmanager',
            region_name=region_name
        )

        try:
            get_secret_value_response = client.get_secret_value(
                SecretId=secret_name
            )
        except Exception as e:
            logging.error(f"Error retrieving secret {secret_name}: {str(e)}")
            raise

        # Depending on whether the secret is a string or binary, one of these fields will be populated.
        if 'SecretString' in get_secret_value_response:
            import json
            try:
                # Explicitly annotate the return type for mypy
                result: Dict[str, Any] = json.loads(get_secret_value_response['SecretString'])
                return result
            except json.JSONDecodeError:
                # If not a JSON, return as a single-key dictionary
                return {"SecretString": get_secret_value_response['SecretString']}
        else:
            import base64
            decoded_binary_secret = base64.b64decode(get_secret_value_response['SecretBinary'])
            return {"SecretBinary": decoded_binary_secret}

### **Quản lý kết nối an toàn**

Hệ thống triển khai cơ chế quản lý kết nối an toàn (secure connection management) nhằm ngăn chặn rò rỉ thông tin xác thực (credential leakage) và đảm bảo quy trình dọn dẹp kết nối (proper cleanup) được thực hiện đúng cách sau mỗi phiên làm việc:

    # From services/aws_service.py - Secure connection cleanup
    async def cleanup(self) -> None:
        """Clean up AWS client resources."""
        try:
            if self.Amazon_Bedrock_client:
                try:
                    await self.Amazon_Bedrock_client.__aexit__(None, None, None)
                except Exception as e:
                    self.logger.error(f"Error closing Amazon Bedrock client: {str(e)}")
                finally:
                    self.Amazon_Bedrock_client = None

            self.logger.info("Successfully cleaned up AWS client resources")
        except Exception as e:
            # Even if cleanup fails, reset the references to avoid stale connections
            self.Amazon_Bedrock_client = None



### **Khắc phục sự cố và gỡ lỗi**

Wrapper API được trang bị khả năng ghi log và gỡ lỗi toàn diện (comprehensive logging and debugging) nhằm hỗ trợ phát hiện và xử lý sự cố một cách nhanh chóng và chính xác. Hệ thống triển khai ghi log chi tiết (detailed logging) xuyên suốt quy trình xử lý yêu cầu (request processing flow). Mỗi yêu cầu đều được gán một mã định danh duy nhất (unique ID) — mã này được sử dụng trong toàn bộ quá trình xử lý để hỗ trợ việc truy vết và phân tích (tracing) khi cần gỡ lỗi hoặc kiểm tra hiệu năng.

    # From core/refactored_chat_bot.py - Request tracing
    request_id = str(id(query))
    start_time = time.perf_counter()

    # Used in all log messages
    self.logger.info(f"[{request_id}] Incoming request received")


### **Bài học kinh nghiệm và thực tiễn tốt nhất**

Thông qua quá trình hợp tác này, nhiều bài học kỹ thuật quan trọng đã được rút ra — có thể mang lại lợi ích cho những nhóm đang thực hiện các dự án tương tự:

* **Configuration-driven architecture** – Việc sử dụng tệp cấu hình thay vì mã hóa trực tiếp hành vi riêng cho từng mô hình mang lại lợi ích to lớn trong bảo trì và mở rộng. Cách tiếp cận này cho phép thêm mô hình mới mà không cần chỉnh sửa mã nguồn, đồng thời giảm đáng kể nguy cơ phát sinh lỗi.  
* **Protocol translation challenges** – Thách thức phức tạp nhất là xử lý các khác biệt tinh tế trong giao thức truyền dữ liệu (streaming) giữa các mô hình khác nhau. Việc xây dựng một lớp trừu tượng ổn định (robust abstraction layer) đòi hỏi xem xét cẩn thận các trường hợp biên (edge cases) và xử lý lỗi toàn diện.  
* **Error normalization** – Để đảm bảo trải nghiệm xử lý lỗi thống nhất giữa các mô hình, nhóm đã xây dựng cơ chế chuẩn hóa lỗi nâng cao, có thể chuyển đổi lỗi đặc thù của từng mô hình thành thông báo thân thiện và dễ hiểu cho người dùng. Cách tiếp cận này cải thiện đáng kể trải nghiệm cho cả nhà phát triển và người dùng cuối.  
* **Type safety** – Việc sử dụng chặt chẽ gợi ý kiểu (type hints) của Python là yếu tố then chốt trong duy trì chất lượng mã nguồn của một codebase phức tạp có nhiều người đóng góp. Cách làm này giảm thiểu lỗi và tăng khả năng bảo trì mã.  
* **Security first** – Tích hợp Secrets Manager ngay từ đầu giúp đảm bảo toàn bộ thông tin xác thực được quản lý an toàn trong suốt vòng đời hệ thống, ngăn ngừa các lỗ hổng bảo mật tiềm ẩn.

### **Kết luận**

Sự hợp tác giữa AWS Generative AI Innovation Center và Quora minh chứng rằng một thiết kế kiến trúc được cân nhắc kỹ lưỡng có thể đẩy nhanh đáng kể tốc độ triển khai và đổi mới AI. Bằng việc xây dựng một wrapper API hợp nhất cho các mô hình Amazon Bedrock, hai nhóm đã rút ngắn thời gian triển khai từ vài ngày xuống chỉ còn vài phút, đồng thời mở rộng danh mục mô hình và cải thiện trải nghiệm người dùng.

Cách tiếp cận này — tập trung vào trừu tượng hóa (abstraction), phát triển dựa trên cấu hình (configuration-driven development), và xử lý lỗi mạnh mẽ (robust error handling) — mang lại những bài học quý giá cho các tổ chức đang tìm cách tích hợp nhiều mô hình AI một cách hiệu quả. Các mẫu thiết kế và kỹ thuật được trình bày trong giải pháp này có thể áp dụng cho nhiều tình huống tích hợp AI khác nhau trong thực tế.

Đối với các lãnh đạo công nghệ và nhà phát triển đang làm việc với các thách thức tương tự, nghiên cứu tình huống này nhấn mạnh giá trị của việc đầu tư vào các framework tích hợp linh hoạt (flexible integration frameworks) thay vì các kết nối điểm-đến-điểm truyền thống. Khoản đầu tư ban đầu vào việc xây dựng một lớp trừu tượng mạnh mẽ sẽ mang lại lợi ích dài hạn trong bảo trì hệ thống và mở rộng năng lực.

### Để tìm hiểu thêm về việc triển khai các giải pháp tương tự, bạn có thể tham khảo:

* [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/) – Hướng dẫn thực hành tốt nhất trong việc xây dựng hạ tầng an toàn, hiệu năng cao, linh hoạt và đáng tin cậy.  
  [Amazon Bedrock Developer Guide](https://docs.aws.amazon.com/bedrock/latest/userguide/what-is-bedrock.html) – Thông tin chi tiết về cách làm việc với các mô hình nền tảng (FMs).  
* [AWS Generative AI Innovation Center](https://aws.amazon.com/generative-ai/innovation-center/) – Nguồn hỗ trợ cho các dự án AI sáng tạo.  
* [AWS Prescriptive Guidance for LLM Deployment](https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/deploy-llms-on-aws.html) – Thực tiễn tốt nhất khi triển khai các mô hình ngôn ngữ lớn (LLMs).

AWS Generative AI Innovation Center và Quora sẽ tiếp tục hợp tác mở rộng framework này, nhằm đảm bảo người dùng Poe luôn được truy cập vào các mô hình AI mới nhất và mạnh mẽ nhất, với thời gian triển khai tối thiểu.

---

**Về các tác giả**

| ![](/images/3-Blog/Blog1/5.png) | Dr. Gilbert V. Lepadatu là Kiến trúc sư Học sâu cao cấp (Senior Deep Learning Architect) tại AWS Generative AI Innovation Center, nơi ông hỗ trợ các doanh nghiệp thiết kế và triển khai các giải pháp GenAI quy mô lớn và tiên tiến. Với bằng Tiến sĩ Triết học (PhD in Philosophy) và hai bằng Thạc sĩ, ông mang đến một cách tiếp cận toàn diện và liên ngành (holistic and interdisciplinary) trong khoa học dữ liệu và trí tuệ nhân tạo. |
| :---- | :---- |
| ![](/images/3-Blog/Blog1/6.jpeg) | **Nick Huber** là Trưởng nhóm Hệ sinh thái AI (AI Ecosystem Lead) cho Poe (thuộc Quora), chịu trách nhiệm đảm bảo việc tích hợp các mô hình AI hàng đầu lên nền tảng Poe diễn ra đúng hạn và đạt chất lượng cao nhất. |

