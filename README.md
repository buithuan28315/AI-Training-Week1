1. TDD – Test-Driven Development
1.1. TDD là gì?
TDD (Test-Driven Development) là một phương pháp phát triển phần mềm trong đó developer viết automated test trước khi viết implementation code.
Thay vì viết chức năng trước rồi mới kiểm tra nó, TDD bắt đầu bằng việc xác định behavior mà phần mềm cần có, viết test để mô tả behavior đó, sau đó mới viết code để đáp ứng test.
TDD thường được thực hiện theo chu trình:
Red → Green → Refactor
Chu trình này được lặp lại liên tục cho từng behavior hoặc requirement nhỏ của hệ thống.
TDD có hai lợi ích chính:
•	Giúp developer làm rõ expected behavior trước khi implementation. 
•	Tạo ra một bộ test có thể được chạy lại để phát hiện regression khi code thay đổi. 
TDD không có nghĩa là chỉ cần viết càng nhiều test càng tốt. Điểm quan trọng là test được sử dụng như một phần của quá trình phát triển, thay vì chỉ được viết sau khi hoàn thành code.
1.2. Red – Green – Refactor
Red
Red là bước đầu tiên.
Developer xác định một behavior mới cần có và viết test để kiểm tra behavior đó. Khi chạy test, test phải fail vì functionality tương ứng chưa được implement hoặc chưa hoạt động đúng.
Mục đích của bước Red là xác nhận rằng test thực sự có khả năng phát hiện trạng thái chưa đúng của chương trình.
Red = Viết test → Test fail.
Green
Sau khi có test fail, developer viết implementation tối thiểu cần thiết để test pass.
Mục tiêu của bước này là làm cho behavior được yêu cầu hoạt động đúng theo test hiện tại. Không nhất thiết phải tối ưu code ngay ở bước này.
Green = Implement → Test pass.
Refactor
Sau khi test pass, developer xem xét và cải thiện code.
Có thể cải thiện:
•	cấu trúc code; 
•	readability; 
•	loại bỏ duplication; 
•	đơn giản hóa logic; 
•	cải thiện maintainability. 
Điều quan trọng là behavior của chương trình không được thay đổi và các test hiện có vẫn phải pass.
Refactor = Cải thiện code → Behavior giữ nguyên → Test vẫn pass.
Sau đó developer tiếp tục với requirement tiếp theo và bắt đầu một vòng Red → Green → Refactor mới.

2. Testing Levels
Testing có thể được thực hiện ở nhiều mức độ khác nhau. Trong phạm vi bài này, ba level quan trọng là:
1.	Unit Testing 
2.	Integration Testing 
3.	End-to-End Testing 
Điểm khác nhau chính giữa chúng là phạm vi được kiểm tra.
2.1. Unit Testing
Unit test kiểm tra một đơn vị nhỏ và có thể kiểm tra độc lập của phần mềm.
Một unit thường có thể là:
•	function; 
•	method; 
•	class; 
•	hoặc một phần logic nhỏ. 
Mục tiêu là xác định xem đơn vị đó có tạo ra kết quả đúng với các input và điều kiện đã xác định hay không.
Unit test thường có đặc điểm:
•	phạm vi nhỏ; 
•	chạy nhanh; 
•	dễ xác định nguyên nhân khi test fail; 
•	thường không phụ thuộc trực tiếp vào database, network hoặc các hệ thống bên ngoài. 
Ví dụ trong Ticket Manager, có thể kiểm tra riêng logic:
Khi người dùng cung cấp một ticket title hợp lệ, hệ thống có tạo ticket với title đó hay không.
Unit Testing = kiểm tra từng phần nhỏ của hệ thống.

2.2. Integration Testing
Integration test kiểm tra sự tương tác giữa nhiều thành phần của hệ thống.
Một component có thể hoạt động đúng khi test riêng nhưng vẫn có thể xảy ra lỗi khi kết hợp với component khác.
Ví dụ:
Ticket Manager → Ticket Service → File Storage
Ta có thể kiểm tra xem khi Ticket Manager tạo một ticket, dữ liệu có thực sự được lưu vào storage đúng định dạng và có thể đọc lại hay không.
Integration testing thường được sử dụng để phát hiện những vấn đề liên quan đến:
•	giao tiếp giữa các module; 
•	database hoặc file storage; 
•	API; 
•	configuration; 
•	integration với external dependencies. 
Integration Testing = kiểm tra các phần của hệ thống có hoạt động đúng khi kết hợp với nhau hay không.
2.3. End-to-End Testing
End-to-End (E2E) testing kiểm tra một workflow hoàn chỉnh của hệ thống, từ đầu đến cuối.
Thay vì kiểm tra một function hoặc một sự kết hợp giữa vài component, E2E test mô phỏng một scenario gần với cách người dùng thực sự sử dụng hệ thống.
Ví dụ với Ticket Manager CLI:
Người dùng nhập command → CLI nhận input → validation → xử lý ticket → lưu dữ liệu → trả kết quả cho người dùng.
E2E testing có phạm vi lớn hơn nên thường:
•	mất nhiều thời gian chạy hơn; 
•	khó xác định nguyên nhân lỗi hơn; 
•	nhưng có khả năng phát hiện những vấn đề mà unit hoặc integration test riêng lẻ không phát hiện được. 
E2E Testing = kiểm tra toàn bộ workflow từ đầu đến cuối.

3. So sánh ba testing levels
	Unit Test	Integration Test	E2E Test
Phạm vi	Một phần nhỏ	Nhiều thành phần kết hợp	Toàn bộ workflow
Mục tiêu	Kiểm tra logic riêng lẻ	Kiểm tra sự tương tác	Kiểm tra hệ thống thực tế
Tốc độ	Nhanh	Trung bình	Thường chậm hơn
Dễ debug	Dễ	Khó hơn	Khó nhất
Ví dụ Ticket Manager	Kiểm tra validation của ticket	Kiểm tra ticket + file storage	Kiểm tra toàn bộ command workflow

Ba loại test không thay thế hoàn toàn cho nhau.
Một hệ thống đáng tin cậy thường sử dụng nhiều mức testing khác nhau: unit test để kiểm tra logic nhỏ, integration test để kiểm tra sự kết hợp giữa các thành phần và E2E test để xác nhận các workflow quan trọng hoạt động đúng từ đầu đến cuối.
4. Mối quan hệ giữa TDD và Testing Levels
Một điểm cần phân biệt:
TDD là development approach, còn Unit / Integration / E2E là các testing levels.
TDD thường được áp dụng mạnh ở unit level vì unit test nhanh và cung cấp feedback nhanh. Tuy nhiên, TDD không đồng nghĩa với việc chỉ được viết unit test.
Trong một dự án thực tế, developer có thể:
Dùng TDD để phát triển từng phần nhỏ → dùng integration tests để kiểm tra sự kết hợp → dùng E2E tests để xác nhận workflow quan trọng.
Nguồn và Tài liệu AI lấy và Sử dụng đã kiểm chứng :
•  Martin Fowler – Test Driven Development 
•  Agile Alliance – Test-Driven Development 
•  Martin Fowler – Practical Test Pyramid

1 Số Nguồn và Tài liệu Thông qua tìm kiếm trên Google dùng để đối chiếu với tài liệu của AI :
Testing Levels
https://www.twilio.com/en-us/blog/unit-integration-end-to-end-testing-difference
https://viblo.asia/p/tim-hieu-ve-cac-cap-do-kiem-thu-test-levels-4P856drAZY3

https://tech.cybozu.vn/cac-cap-do-kiem-thu-phan-mem-test-levels-d86e8/

https://viblo.asia/p/so-sanh-giua-3-co-che-test-trong-ung-dung-nestjs-PwlVmbxm45Z

Test Driven Development (TDD)


https://viblo.asia/p/tong-quan-ve-tdd-gDVK2WzeZLj
https://viblo.asia/p/kien-thuc-co-ban-ve-tdd-test-driven-development-Do754AWLKM6


AI Validation – How tests help verify and improve AI-generated code

Code do AI sinh ra không nên được mặc định là đúng. Test có thể được sử dụng như một lớp kiểm chứng để xác định code có thực hiện đúng yêu cầu và hành vi mong muốn hay không.

Verify: Chạy test để phát hiện lỗi, hành vi sai hoặc các trường hợp AI bỏ sót.
Improve: Khi test thất bại, kết quả test cung cấp phản hồi để developer xác định vấn đề và sửa code.
Validate AI-generated tests: Không chỉ kiểm tra code do AI tạo ra, mà cũng cần xem xét test do AI viết. Một test có thể “pass” nhưng assertion quá yếu hoặc không kiểm tra đúng yêu cầu.
Human review: Test không đảm bảo code hoàn toàn chính xác. Developer vẫn cần kiểm tra logic, yêu cầu nghiệp vụ, security và chất lượng của cả code lẫn test.

Kết luận:
Testing giúp biến AI-generated code từ thứ “AI cho rằng đúng” thành thứ có thể kiểm chứng bằng hành vi thực tế. Tuy nhiên, testing là một lớp validation chứ không thay thế hoàn toàn việc review của developer.
Nguồn Và tài Liệu :

https://github.com/github/docs/blob/main/content/copilot/tutorials/review-ai-generated-code.md?
https://www.linkedin.com/pulse/understanding-basics-ai-testing-validaitor-89bbe/
CLI Testing – What should be tested in a CLI tool?
CLI (Command-Line Interface) là giao diện dạng văn bản cho phép người dùng tương tác với phần mềm thông qua các câu lệnh, tùy chọn và tham số trong terminal. Một CLI thường hoạt động theo quy trình Input → Process → Output: nhận lệnh từ người dùng, xử lý yêu cầu và trả về kết quả hoặc thông báo lỗi.
Để xây dựng một CLI đáng tin cậy, cần kiểm thử các hành vi mà người dùng có thể thực hiện, bao gồm:
•	Commands và arguments: Kiểm tra các câu lệnh và tham số hợp lệ, không hợp lệ hoặc bị thiếu.
•	Validation: Kiểm tra dữ liệu đầu vào và các trường hợp dữ liệu không đúng định dạng.
•	Output và errors: Đảm bảo chương trình trả về kết quả chính xác và thông báo lỗi rõ ràng.
•	File operations: Kiểm tra việc tạo, đọc, sửa đổi và xóa file nếu CLI có thao tác với file.
•	Edge cases: Kiểm tra các trường hợp đặc biệt hoặc dữ liệu bất thường.
•	Safety: Kiểm thử các command trong môi trường an toàn trước khi sử dụng trong môi trường production, đặc biệt với những command có thể thay đổi hoặc xóa dữ liệu.
Test case cho Ticket Manager CLI
Nhóm	Input	Expected
Command hợp lệ	ticket add "Fix bug"	Tạo ticket, exit code 0
Validation	ticket add (thiếu title)	Error rõ ràng, exit code 1
File storage	Add → restart CLI → list	Ticket vẫn còn sau khi chạy lại
Error handling	ticket delete 999 (ID không tồn tại)	Error "Not found", không crash

Nguồn và tài liệu tham khảo:

https://fptshop.com.vn/tin-tuc/danh-gia/cli-la-gi-166731

https://github.com/resources/articles/what-is-a-cli

5. Common Testing Mistakes
Trong quá trình áp dụng TDD, có một số lỗi phổ biến có thể làm giảm giá trị của test.
5.1. Over-testing
Over-testing xảy ra khi developer viết quá nhiều test cho những trường hợp không mang lại nhiều giá trị hoặc kiểm tra cùng một behavior nhiều lần.
Điều này làm test suite:
•	khó bảo trì;
•	chạy lâu hơn;
•	tốn thời gian viết và cập nhật test;
•	khiến developer tập trung quá nhiều vào test thay vì behavior quan trọng.
Nên ưu tiên kiểm tra các behavior quan trọng, business rules và edge cases thay vì cố gắng test mọi dòng code.
5.2. Weak Assertions
Weak assertions xảy ra khi test có chạy nhưng kiểm tra quá ít hoặc không kiểm tra đúng kết quả mong đợi.
Ví dụ, test chỉ kiểm tra rằng một function không throw error nhưng không kiểm tra giá trị trả về có chính xác hay không.
Một test tốt cần có assertion đủ cụ thể để phát hiện implementation sai.
5.3. Testing Implementation Details
Test nên tập trung vào behavior của hệ thống thay vì cách code được implement bên trong.
Nếu test phụ thuộc quá nhiều vào internal implementation, việc refactor code có thể làm test fail mặc dù behavior của chương trình vẫn đúng.
Vì vậy, nên ưu tiên kiểm tra:
Input → Behavior → Expected Output
thay vì kiểm tra trực tiếp cấu trúc hoặc những chi tiết implementation không quan trọng đối với người dùng.
5.4. Blindly Trusting AI Output
Khi sử dụng AI để hỗ trợ viết code hoặc test, không nên mặc định rằng output của AI là chính xác.
AI có thể:
•	hiểu sai requirement;
•	bỏ sót edge cases;
•	tạo assertion quá yếu;
•	tạo test chỉ phù hợp với implementation hiện tại;
•	tạo code hoặc test có lỗi nhưng vẫn có vẻ hợp lý.
Do đó, developer cần review requirement, code và test, sau đó chạy test để kiểm chứng behavior thực tế.
Test cũng cần được kiểm tra về chất lượng, vì một test pass không đồng nghĩa với việc implementation đã đúng hoàn toàn.
Kết luận
Các lỗi trên có thể làm test suite trở nên tốn kém nhưng vẫn không cung cấp đủ sự đảm bảo về chất lượng. Khi kết hợp TDD với AI, developer nên tập trung vào behavior quan trọng, assertion rõ ràng và validation thực tế, đồng thời không phụ thuộc hoàn toàn vào code hoặc test do AI tạo ra.
Nguồn và tài liệu tham khảo: 
https://martinfowler.com/articles/practical-test-pyramid.html
https://martinfowler.com/bliki/AssertionFreeTesting.html
https://martinfowler.com/articles/practical-test-pyramid.html
https://docs.github.com/en/copilot/tutorials/review-ai-generated-code
https://docs.github.com/en/copilot/tutorials/write-tests


6. Evidence of Applying the 3 Workflows
6.1. Layered Questioning
Quá trình research được thực hiện bằng cách đặt câu hỏi theo từng mức độ, từ khái quát đến cụ thể:
•	Research: TDD là gì và TDD có thể được sử dụng như thế nào để xây dựng CLI tool đáng tin cậy với sự hỗ trợ của AI?
•	Brief: Những nội dung chính nào cần được trình bày về TDD, testing levels, AI validation và CLI testing?
•	Example: Với một Ticket Manager CLI, những trường hợp nào cần được kiểm thử?
•	Validation: Nội dung này có đáp ứng đầy đủ yêu cầu và Acceptance Criteria của homework không?
Cách đặt câu hỏi theo từng bước giúp chuyển từ việc tìm hiểu khái niệm sang áp dụng vào ví dụ và cuối cùng kiểm tra lại kết quả.
________________________________________
6.2. Solution Exploration
Trong quá trình research, nhiều nguồn và cách tiếp cận được xem xét trước khi lựa chọn nội dung đưa vào tài liệu.
Một số câu hỏi được sử dụng:
•	Có những nguồn hoặc tài liệu đáng tin cậy nào có thể dùng để kiểm chứng nội dung về testing?
•	Nguồn GitHub này nói gì về CLI và những khía cạnh nào của CLI cần được kiểm thử?
•	Có thể viết phần CLI Testing dựa trực tiếp trên nội dung của nguồn GitHub này như thế nào?
•	Những nguồn nào phù hợp để làm dẫn chứng cho các lỗi phổ biến trong testing như over-testing, weak assertions và testing implementation details?
Sau khi xem xét các nguồn, những nội dung phù hợp với phạm vi của homework được lựa chọn để đưa vào research document.
________________________________________
6.3. Iterative Refinement
Research document được cải thiện qua nhiều vòng review và chỉnh sửa thay vì sử dụng ngay kết quả đầu tiên của AI.
Một số câu hỏi thể hiện quá trình này:
•	Nội dung research hiện tại đã đáp ứng đầy đủ yêu cầu của homework và Acceptance Criteria chưa?
•	Phần Common Testing Mistakes đã bao quát đủ bốn vấn đề mà đề bài yêu cầu chưa?
•	Có nguồn tài liệu nào có thể dùng để dẫn chứng cho phần Common Testing Mistakes không?
•	Có thể trình bày evidence của ba workflow dựa trên chính các câu hỏi và cách thực hiện research không?
Sau mỗi lần review, nội dung được bổ sung, chỉnh sửa hoặc thay đổi cách trình bày dựa trên feedback và kết quả kiểm chứng.
Quá trình có thể được tóm tắt:
AI suggestion → Review → Feedback → Refinement → Validation

