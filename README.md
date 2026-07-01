# Abyss-Walker-CLI
Đồ án cuối kỳ môn Cấu trúc dữ liệu &amp; Giải thuật - C++ CLI.
## Tên ứng dụng
**Maze Game Pathfinding** - Đồ án cuối kỳ Cấu trúc Dữ liệu & Giải thuật.
Trò chơi tạo mê cung ngẫu nhiên và so sánh trực quan hiệu năng của các thuật toán tìm đường (BFS, DFS, A*).

## Cấu trúc dữ liệu sử dụng
- **2D Array / Graph:** Dùng để lưu trữ bản đồ mê cung (lưới tọa độ). Cho phép truy xuất nhanh các ô xung quanh (O(1)).
- **Stack:** Dùng để sinh mê cung (DFS Recursive Backtracker) và giải mê cung (DFS Pathfinding) vì tính chất LIFO hỗ trợ cơ chế Quay lui (Backtracking).
- **Queue:** Dùng để tìm đường ngắn nhất (BFS) vì tính chất FIFO giúp thuật toán loang đều ra mọi hướng cùng một lúc.
- **Priority Queue (Min-Heap):** Dùng cho thuật toán tìm đường A*. Sắp xếp ưu tiên các Node có tổng chi phí dự đoán thấp nhất lên đầu để duyệt trước, giúp tìm đường tối ưu bộ nhớ hơn BFS.

## Compile và chạy
**Chạy ứng dụng chính:**
g++ -std=c++17 src/main.cpp src/functions.cpp -o app && ./app

**Chạy file Kiểm thử (Unit Tests):**
g++ -std=c++17 tests/test_cases.cpp src/functions.cpp -o test_app && ./test_app

## Chức năng
1. Hiển thị Mê cung trực quan trên Terminal.
2. Sinh mê cung ngẫu nhiên không có vòng lặp (Perfect Maze).
3. Người chơi tự giải bằng phím W/A/S/D.
4. Tự động tìm đường ngắn nhất bằng BFS.
5. Tự động tìm đường bằng DFS (thể hiện sự vòng vèo do backtracking).
6. Tự động tìm đường bằng A* (Dùng Priority Queue và Heuristic Manhattan).
7. So sánh hiệu năng (số bước đi) giữa BFS và DFS.
8. Bẫy lỗi nhập sai trên Menu và điều chỉnh kích thước tùy ý.

## Test cases
Đã triển khai 5 test case chính sử dụng `<cassert>`:
1. `test_khoi_tao_me_cung`: Đảm bảo mê cung sinh ra luôn hợp lệ và có đường đi.
2. `test_bfs_tim_duong_luon_co_loi_giai`: Test khả năng chạy trên ma trận lớn (51x51).
3. `test_so_sanh_bfs_va_dfs`: Đảm bảo chiều dài đường đi BFS <= DFS.
4. `test_a_star_toi_uu`: Đảm bảo A* tìm ra kết quả chính xác bằng với BFS.
5. `test_edge_case_kich_thuoc_nho`: Test nhập kích thước chẵn và nhỏ (4x4), hệ thống tự fix thành (5x5) và không crash.

## Cấu trúc file
src/
   main.cpp         - Menu, điều khiển vòng lặp và bẫy lỗi input
   structures.h     - Khai báo struct (Point, AStarNode) và nguyên mẫu class Maze
   functions.cpp    - Cài đặt chi tiết các thuật toán DFS, BFS, A*
tests/
   test_cases.cpp   - Chứa 5 kịch bản kiểm thử tự động
README.md           - Tài liệu báo cáo project

# Abyss-Walker-CLI (Đồ án Giải Mê Cung)

## 1. Giới thiệu chi tiết đồ án
- **Sản phẩm:** Game sinh mê cung và tìm đường tự động trên giao diện Terminal (Console).
- **Cốt lõi:** Sử dụng mảng 2 chiều (Graph) để tạo bản đồ. Áp dụng 3 thuật toán duyệt đồ thị (DFS, BFS, A*) để đục tường tạo đường đi và tìm lối thoát.
- **Điểm nhấn:** Menu cho phép người dùng tự chơi, hoặc chạy máy tự động để so sánh hiệu năng (số bước đi) giữa các thuật toán với nhau.

## 2. Lý do chọn đề tài
- Để trực quan hóa các cấu trúc dữ liệu khô khan: Nhìn thấy được `Stack` và `Queue` chạy trên màn hình thực tế ra sao thay vì chỉ in ra các con số.
- Để hiểu bản chất của các ứng dụng chỉ đường (như Google Maps): Trả lời được câu hỏi tại sao phải dùng BFS hoặc A* để tìm đường, chứ tuyệt đối không dùng DFS.

## 3. Lấy thông tin từ đâu trong code để áp dụng?
- **Khung bản đồ:** Lưu trữ ở biến `vector<vector<char>> grid`. Ký hiệu `#` là tường, dấu cách là đường đi.
- **Thuật toán sinh bản đồ:** Nằm ở hàm `generateMazeDFS()`. Áp dụng **Stack** để đi sâu đục tường, đụng ngõ cụt thì lấy (pop) tọa độ cũ ra để quay lui.
- **Thuật toán tìm đường ngắn nhất:** Nằm ở hàm `solveBFS()`. Áp dụng **Queue** để loang đều ra mọi hướng cùng lúc (như vết dầu loang), đụng đích trước là đường ngắn nhất.
- **Thuật toán thông minh:** Nằm ở hàm `solveAStar()`. Áp dụng **Priority Queue** để ưu tiên đi vào các ô có xu hướng gần đích nhất (dùng công thức khoảng cách Manhattan).

## 4. Hướng phát triển kế tiếp
- **Về giao diện:** Thoát khỏi Console, tích hợp các thư viện đồ họa (như SFML/Raylib) để làm game 2D hoàn chỉnh có hình ảnh nhân vật.
- **Về tính năng:** Thêm cơ chế "Sương mù" (Người chơi chỉ nhìn thấy bán kính 3 ô xung quanh) để tăng độ khó khi tự giải.

## 5. Ghi chú bảo vệ
Thay vào đó, hãy thẳng thắn thừa nhận có dùng tài liệu cú pháp, nhưng **nắm chắc luồng logic**. 

Chỉ cần nhớ 3 câu "thần chú" này để giải thích bất kỳ đoạn code nào trong các vòng lặp:
1. Gặp lệnh `push`: "Chỗ này đưa tọa độ ô tiếp theo vào hàng đợi/ngăn xếp để chuẩn bị duyệt."
2. Gặp lệnh `if (grid[r][c] == '#')`: "Chỗ này check va chạm, nếu là tường thì bỏ qua không đi."
3. Gặp mảng `visited`: "Chỗ này đánh dấu ô đã đi qua để thuật toán không bị kẹt trong vòng lặp vô hạn."
