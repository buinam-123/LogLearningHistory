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
                * `git reset HEAD~1`: Nếu muốn hủy commit và ddauw các thay đổi trở lại Working Directory (Không còn Staged) có nghĩa là đưa trở về trạng thái mới thay đổi(code) chưa add chưa commit chưa gì hết
                * `git reset --hard HEAD~1`: dùng để xóa bỏ hoàn toàn commit gần nhất và đưa toàn bộ dự án quay trở về trạng thái của commit ngay trước đó.
# test `git reset --hard HEAD~1`
