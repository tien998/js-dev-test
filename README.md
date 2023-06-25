# js-dev-test
 ### Thông tin phiên bản:
    fastify: last version
    nodeJS: 18.16.0
    Nextjs (React) được đặt trong thư mục `Book_app_NextJS`
    @elastic/elasticsearch: 8.8.1

 ### Khởi chạy:
   ### Node:
    Thay đổi thông tin kết nối Elastic Server tại `services/elasticService.js` các dòng 4:8
    Chạy lệnh`node app.js` khởi chạy chương trình
    API được truy cập qua `http://localhost:3001/book`
    Thêm dữ liệu mẫu bằng cách truy cập `http://localhost:3001/seedDocs` hoặc chạy lệnh `node axios/seedDocs.js` 
   ### React:
    Truy cập vào thư mục `Book_app_NextJS`
    Để đảm bảo NextJS chạy có thể khởi chạy, xin hãy đảm bảo fastify và elastic đã khởi chạy và tại Nextjs đã thực thi các lệnh sau:
     npm install
     npm run build 
    Chạy lệnh ` npm run start` để NextJS khởi chạy và lắng nghe ở `http://localhost:3000/`
    Chọn cuốn sách muốn xem chi tiết trong danh sách sách và có thể viết bình luận.
    Bình luận sách sử dụng socket.io để gửi và hiển thị.
    Nội dung bình luận tạm thời được lưu vào 1 mảng trên Fastify, em sẽ tiếp tục cập nhật thêm tính năng cho bình luận lưu ở Elastics

 ### Kiểm thử bằng Axios:
    Trong thư mục dự án, có thể dùng Axios để kiểm thử API bằng các lệnh sau, xem kết quả trả về ở terminal
    `node axios/getall.js ` Lấy toàn bộ dữ liệu
    `node axios/get.js ` Lấy dữ liệu dựa trên 1 id cụ thể, có thể chỉnh sửa tham số id trong `axios/get.js`
    `node axios/put.js ` Sửa tài liệu dựa trên id cụ thể, có thể chính sửa id và giá trị trong tại liệu trong `axios/put.js`
    `node axios/post.js ` Tạo tài liệu mới trên Elastic có thể chỉnh sửa giá trị tài liệu trong `axios/post.js`
    
 ### Giải thích NodeJS:
    API được định tuyến (Routing) tại file 'app.js'gồm các phương thức GET, PUT, POST. 
    Các lệnh thao tác và thông tin kết nối với Elastic được đặt trong `services/elasticService.js` và được gọi bởi các phương thức trong `app.js`

    Dữ liệu được xác thực tính hợp lệ bằng JSON Schema trước khi POST hoặc PUT lên server được cấu hình tại dòng 7 file `app.js` như sau:
    
    const validateSchema = {
    schema: {
        body: {
            type: 'object',
            properties: {
                id: { type: 'number' },
                title: { type: 'string' },
                author: { type: 'string' },
                publishedDate: { type: 'string' },
                description: { type: 'string' },
                price: { type: 'number' }
            }
        }
      } 
    }

 ### 
    

 ### Trên đây là phần NodeJS viết trên nền tảng Fastify lấy dữ liệu từ Elastic Server
 ### Phần ReactJS em làm bằng NextJS đang trong quá trình hoàn thành và sẽ bổ sung vào ngày 23/6 (ngày mai)
    