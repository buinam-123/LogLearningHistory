# Ngày 13/11/2026 (Hôm nay là sinh nhật tôi "Bùi Thành Nam")
- Học lệnh git hub đẩy lên remote
- Đẩy hết bài hôm nay học lên github và lưu trữ lại vào file log.md để xem mình đã làm gì
- `cố gắng học được nhiều hơn để không phí thời gian`
- learning 
    + git rm -r cache folder/file..... Xóa `Tham số --cached cực kỳ quan trọng để không làm mất dữ liệu thật trên máy bạn`
    
    + Ban đầu: 
        + Khi xog dự án và ta dùng "git init" để tạo file .git đầu tiên để quản lý --> sau đó ta bấm "git status" nó sẽ hiện ra những thứ chưa được quản lý và mới toanh đã trong đó
        + lúc này ta cần `git add ., git add <file>` để thêm dữ liệu và đẩy lên Staged từ máy cá nhân (working directory)
        + sau khi chạy lệnh `git add` thì `git status` sẽ hiển thị toàn bộ file đó dưới mục "Changes to be commited"(những file cần được commit) 
            - nếu không muốn giữ file trong staged ta có thể `git restore --staged <file>`
            - khi restore xog thì `git status` lại hiện những file cần được đưa lên Staged
        + Sau đó ta `git commit -m "text"` thì sẽ đẩy được lên Local Repo
            - Nếu trong trường hợp không muốn giữ nó hay muốn xóa file đó khỏi Local Repo thì dùng 
                * `git reset --soft HEAD~1`: Hủy commit gần nhất , giữ nguyên những thay đổi trong Staging Are, Không xóa file trên máy tính 
                * `git reset HEAD~1`: Nếu muốn hủy commit và đưa các thay đổi trở lại Working Directory (Không còn Staged) có nghĩa là đưa trở về trạng thái mới thay đổi(code) chưa add chưa commit chưa gì hết
                * `git reset --hard HEAD~1`: dùng để xóa bỏ hoàn toàn commit gần nhất và đưa toàn bộ dự án quay trở về trạng thái của commit ngay trước đó. (có thể ctrl + Z lại :) hehe
                * `git reset --hard HEAD~2`: sẽ xóa sạch cả 2 commit gần nhất và đưa toàn bộ thư mục dự án trên máy quay về nguyên trạng tại thời điểm của commit HEAD~2.
                <chú ý: dùng --hard có thể mất dữ liệu ở những file khác, có thể ctrl + z được nhưng mà hơi khổ>
            - Xem lịch sử ở từng commit 
                * `git log -p`: Cách đọc kết quả: Những dòng có dấu + màu xanh lá là code mới được thêm vào, còn những dòng có dấu - màu đỏ là code đã bị xóa đi.
                * `git log` (có thể alias): trả về tất cả commit
                * `git log --oneline`: trả về lịch sử commit trên 1 dòng 
                * `git log --stat` (Xem nhật ký kèm theo số liệu thống kê thay đổi): Nếu bạn chỉ muốn biết ở mỗi commit có những file nào bị sửa và sửa bao nhiêu dòng mà không muốn hiện chi tiết code làm rối mắt
                * `git show a1b2c3d`: Lệnh này sẽ hiển thị thông tin tác giả, ngày giờ, lời nhắn commit và toàn bộ nội dung code đã thay đổi duy nhất trong commit đó.
                * `git show`              # commit mới nhất (HEAD)
                * `git show HEAD~2`       # commit cách HEAD 2 bước về trước
                * Các lệnh xem lịch sử khác
                    `git log`                                   # đầy đủ: hash, tác giả, ngày, message (nhấn q để thoát)
                    `git log --oneline`                         # mỗi commit 1 dòng — dùng nhiều nhất
                    `git log --oneline --graph --all`           # vẽ cây nhánh bằng ký tự — RẤT nên nhớ
                    `git log -5`                                # 5 commit gần nhất
                    `git log --author="Nam"`                    # lọc theo tác giả
                    `git log -- index.html`                     # chỉ commit có động đến file này
                    `git log -p`                                # kèm luôn nội dung diff của từng commit
                    `git log --since="2 weeks ago"`             # theo thời gian
                
        + Sau đó ta đẩy lên "Remote Repo" bằng `git push` <Ở Phần 2>
    + Bài tập: 
        <!-- - 1. Tạo repo
        mkdir hoc-git && cd hoc-git
        git init
        git status                         # Quan sát: "No commits yet", không có gì

        - 2. Tạo .gitignore trước tiên
        echo "secret.txt" > .gitignore
        echo "mat khau la 123" > secret.txt
        git status                         # Quan sát: chỉ thấy .gitignore, KHÔNG thấy secret.txt → ignore hoạt động

        - 3. Commit đầu tiên
        git add .gitignore
        git commit -m "Thêm .gitignore"

        - 4. Tạo file và quan sát từng khu vực
        echo "<h1>Xin chao</h1>" > index.html
        git status                         # index.html: Untracked (đỏ)
        git add index.html
        git status                         # index.html: Changes to be committed (xanh)
        git commit -m "Tạo trang chủ"

        - 5. Sửa file, so sánh diff 2 kiểu
        echo "<p>Toi la Nam Tron</p>" >> index.html
        git diff                           # thấy dòng +<p>... 
        git diff --staged                  # TRỐNG — vì chưa add
        git add index.html
        git diff                           # TRỐNG — vì đã add hết
        git diff --staged                  # thấy dòng +<p>...
        git commit -m "Thêm lời giới thiệu vào trang chủ"

        - 6. Xem lịch sử
        git log --oneline                  # thấy 3 commit
        git show HEAD~1                    # xem commit "Tạo trang chủ" -->

----------------------------------DONE------------------------------------------
        + Câu hỏi thêm: 
            - Ở bước 5, tại sao git diff và git diff --staged cho kết quả ngược nhau trước và sau add?
                -> Bỏi vì khi trước khi add thì working directory nhận thấy sự thay đổi và khi ta `git diff` thì sẽ nhận thấy sự thay đổi nó thêm một dòng mới (bản thân git status cũng thấy) và vì đây là trước khi add nên chưa có gì được đẩy lên Staged area nên là khi `git diff --staged`  sẽ không thấy gì hết, nhưng sau khi đẩy lên Staged (bằng add) thì phần working directory sẽ không còn thấy sự thay đổi đó, do đó khi ta `git diff` thì sẽ không thấy sự thay đổi nào mới nữa, mà nó chuyển lên cho Staged lo liệu, khi này ta dùng `git diff --staged` thì nó phát hiện ra sự thay đổi thêm một dòng mới và nó báo ra. nếu như ta commit là khi `git diff --staged` chẳng còn cái quái gì nữa.
            - Nếu bạn add index.html, sau đó sửa tiếp index.html rồi commit, phần sửa sau có vào commit không? (Thử luôn để kiểm chứng!)
                -> giả định đã commit hết mọi thứ trống và không có gì. Ta thay đổi lần đầu tiên trong index.html, và sau đó add nó lên Staged area, rồi ta lại sửa lần thứ 2 ở index.html, cuối cùng ta commit file index.html: bản chất ở dây commit là quá trình đưa dữ liệu từ Staged lên local repo, vậy thì code thay đổi phải có trong staged thì mới đưa được lên local repo thông qua commit, do đó quá trình sửa lần thứ 2 chưa được add nên nó không được commit
            - secret.txt có nằm trong commit nào không? Kiểm tra bằng git show --stat HEAD~2
                -> Vì ta đã dùng gitignore và phớt lờ file secret.txt do đó nó không dược git đả động đến. cho dù ta có dùng `git add .`
                <Ngoại lệ>: 
                    Ví dụ:
                    - Ban đầu secret.txt chưa bị ignore, bạn git add và commit nó.
                    - Sau đó bạn thêm secret.txt vào .gitignore.
                    - Git vẫn tiếp tục theo dõi file này.
                    - Muốn ngừng tracking nhưng vẫn giữ file trên máy, bạn dùng: `git rm --cached secret.txt` với folder thì `git rm -r --cached folder/`


            





