# Ngày 13/11/2026 (Hôm nay là sinh nhật tôi "Bùi Thành Nam")

- Học lệnh git hub đẩy lên remote
- Đẩy hết bài hôm nay học lên github và lưu trữ lại vào file log.md để xem mình đã làm gì
- `cố gắng học được nhiều hơn để không phí thời gian`

## Learning

- `git rm -r cache folder/file.....` Xóa `Tham số --cached cực kỳ quan trọng để không làm mất dữ liệu thật trên máy bạn`
- Khi chạy `git remote add origin https://github.com/user/project.git`

  → thì Git hiểu rằng:
  - `origin`: Tên bí danh tự đặt
  - `https://github.com/user/project.git`: địa chỉ repository trên GitHub
  - git lưu thông tin này trong cấu hình của repo local
  - nếu dùng `git remote -v` thì sẽ có:

  ```text
  origin  https://github.com/user/project.git (fetch)
  origin  https://github.com/user/project.git (push)
  ```

- `origin/main`, `origin/feature-login` (Nhánh remote-tracking): Lưu ý: Đây không phải những nhánh đang trực tiếp chạy trên GitHub. Chúng là các tham chiếu được lưu trong máy tính của bạn để theo dõi trạng thái remote.

### Ban đầu

- Khi xong dự án và ta dùng `git init` để tạo file `.git` đầu tiên để quản lý → sau đó ta bấm `git status` nó sẽ hiện ra những thứ chưa được quản lý và mới toanh đã trong đó
- Lúc này ta cần `git add .`, `git add <file>` để thêm dữ liệu và đẩy lên Staged từ máy cá nhân (working directory)
- Sau khi chạy lệnh `git add` thì `git status` sẽ hiển thị toàn bộ file đó dưới mục "Changes to be commited" (những file cần được commit)
  - Nếu không muốn giữ file trong staged ta có thể `git restore --staged <file>`
  - Khi restore xong thì `git status` lại hiện những file cần được đưa lên Staged
- Sau đó ta `git commit -m "text"` thì sẽ đẩy được lên Local Repo
  - Nếu trong trường hợp không muốn giữ nó hay muốn xóa file đó khỏi Local Repo thì dùng:
    - `git reset --soft HEAD~1`: Hủy commit gần nhất, giữ nguyên những thay đổi trong Staging Are, Không xóa file trên máy tính
    - `git reset HEAD~1`: Nếu muốn hủy commit và đưa các thay đổi trở lại Working Directory (Không còn Staged) có nghĩa là đưa trở về trạng thái mới thay đổi(code) chưa add chưa commit chưa gì hết
    - `git reset --hard HEAD~1`: dùng để xóa bỏ hoàn toàn commit gần nhất và đưa toàn bộ dự án quay trở về trạng thái của commit ngay trước đó. (có thể ctrl + Z lại :) hehe)
    - `git reset --hard HEAD~2`: sẽ xóa sạch cả 2 commit gần nhất và đưa toàn bộ thư mục dự án trên máy quay về nguyên trạng tại thời điểm của commit HEAD~2.

    > <chú ý: dùng --hard có thể mất dữ liệu ở những file khác, có thể ctrl + z được nhưng mà hơi khổ>

  - Xem lịch sử ở từng commit:
    - `git log -p`: Cách đọc kết quả: Những dòng có dấu + màu xanh lá là code mới được thêm vào, còn những dòng có dấu - màu đỏ là code đã bị xóa đi.
    - `git log` (có thể alias): trả về tất cả commit
    - `git log --oneline`: trả về lịch sử commit trên 1 dòng
    - `git log --stat` (Xem nhật ký kèm theo số liệu thống kê thay đổi): Nếu bạn chỉ muốn biết ở mỗi commit có những file nào bị sửa và sửa bao nhiêu dòng mà không muốn hiện chi tiết code làm rối mắt
    - `git show a1b2c3d`: Lệnh này sẽ hiển thị thông tin tác giả, ngày giờ, lời nhắn commit và toàn bộ nội dung code đã thay đổi duy nhất trong commit đó.
    - `git show` # commit mới nhất (HEAD)
    - `git show HEAD~2` # commit cách HEAD 2 bước về trước
    - Các lệnh xem lịch sử khác:

      ```bash
      git log                                   # đầy đủ: hash, tác giả, ngày, message (nhấn q để thoát)
      git log --oneline                         # mỗi commit 1 dòng — dùng nhiều nhất
      git log --oneline --graph --all           # vẽ cây nhánh bằng ký tự — RẤT nên nhớ
      git log -5                                # 5 commit gần nhất
      git log --author="Nam"                    # lọc theo tác giả
      git log -- index.html                     # chỉ commit có động đến file này
      git log -p                                # kèm luôn nội dung diff của từng commit
      git log --since="2 weeks ago"             # theo thời gian
      ```

- Sau đó ta đẩy lên "Remote Repo" bằng `git push` <Ở Phần 2>

## Bài tập

### Câu hỏi thêm

- Ở bước 5, tại sao `git diff` và `git diff --staged` cho kết quả ngược nhau trước và sau add?
  - → Bỏi vì khi trước khi add thì working directory nhận thấy sự thay đổi và khi ta `git diff` thì sẽ nhận thấy sự thay đổi nó thêm một dòng mới (bản thân `git status` cũng thấy) và vì đây là trước khi add nên chưa có gì được đẩy lên Staged area nên là khi `git diff --staged` sẽ không thấy gì hết, nhưng sau khi đẩy lên Staged (bằng add) thì phần working directory sẽ không còn thấy sự thay đổi đó, do đó khi ta `git diff` thì sẽ không thấy sự thay đổi nào mới nữa, mà nó chuyển lên cho Staged lo liệu, khi này ta dùng `git diff --staged` thì nó phát hiện ra sự thay đổi thêm một dòng mới và nó báo ra. nếu như ta commit là khi `git diff --staged` chẳng còn cái quái gì nữa.

- Nếu bạn add `index.html`, sau đó sửa tiếp `index.html` rồi commit, phần sửa sau có vào commit không? (Thử luôn để kiểm chứng!)
  - → giả định đã commit hết mọi thứ trống và không có gì. Ta thay đổi lần đầu tiên trong `index.html`, và sau đó add nó lên Staged area, rồi ta lại sửa lần thứ 2 ở `index.html`, cuối cùng ta commit file `index.html`: bản chất ở đây commit là quá trình đưa dữ liệu từ Staged lên local repo, vậy thì code thay đổi phải có trong staged thì mới đưa được lên local repo thông qua commit, do đó quá trình sửa lần thứ 2 chưa được add nên nó không được commit

- `secret.txt` có nằm trong commit nào không? Kiểm tra bằng `git show --stat HEAD~2`
  - → Vì ta đã dùng gitignore và phớt lờ file `secret.txt` do đó nó không dược git đả động đến. cho dù ta có dùng `git add .`
  - <Ngoại lệ>:
    - Ví dụ:
      - Ban đầu `secret.txt` chưa bị ignore, bạn `git add` và commit nó.
      - Sau đó bạn thêm `secret.txt` vào `.gitignore`.
      - Git vẫn tiếp tục theo dõi file này.
      - Muốn ngừng tracking nhưng vẫn giữ file trên máy, bạn dùng: `git rm --cached secret.txt` với folder thì `git rm -r --cached folder/`

## Phần 2: Đẩy code lên GitHub

### 1. Trường hợp 1: Push lần đầu một nhánh lên GitHub

- `git init`: khỏi tạo git
- `git add .`: đưa thay đổi lên Staged
- `git commit -m "initial commit"`: đẩy thay đổi từ staged lên local repo
- `git branch -M main`: đổi tên đúng với branch trên github
- `git remote add origin https://github.com/user/project.git`: thông báo cho local biết cần đẩy thay đổi lên repo nào của github
- `git push -u origin main`: đẩy code và thiết lập upstream
  - → upstream: trong git là mối liên kết giữa branch local (nhánh trên máy tính) và branch remote (nhánh trên github) tương ứng (giống như một cái cầu được lưu ở đó vậy, ko cần khai báo đích)
  - → Git biết rằng nhánh `main` trên máy tính của bạn đang làm việc với nhánh `main` trên GitHub

### 2. Trường hợp 2: sau khi đã làm lần đầu

- Sau khi đã dùng `git push -u origin main` (đã tạo upstream)
- `git add.`
- `git commit -m "commit"`
- `git push`
- → Git đã ghi nhớ nhánh đích thông qua upstream.

### 3. Trường hợp 3: Tạo nhánh mới rồi push lên GitHub

- `git switch -c feature-login`: Lệnh này vừa tạo vừa switch sang nhánh mới
  - Nếu không dùng thì:
    - `git branch <ten branch>`: tạo branch nhưng vẫn ở branch hiện tại
    - `git switch <ten branch>`: chuyển branch
- `git add.`
- `git commit -m "add login feature"`
- `git push -u origin feature-login`: tạo upstream chỉ định đích là feature-login branch
- → Lần sau chỉ cần đứng ở `<feature-login>` và `git push`

### 4. Trường hợp 4: Local chưa có branch như trên remote

- Nếu như bạn lên github và tạo mới branch vd: `feature-login`
- Thì phía local chưa có `feature-login`.
- Ta cần: `git fetch origin`: để đồng bộ branch trên remote <là lệnh dùng để tải toàn bộ các commit, branch, tag và thông tin mới từ kho lưu trữ từ xa (remote repository có tên là origin) về máy tính của bạn, nhưng không làm thay đổi hay gộp (merge) bất cứ thứ gì vào thư mục làm việc (working directory) hay nhánh local hiện tại của bạn>
- Sau đó: `git switch --track origin/feature-login` : <--track dùng để tạo upstream đầu cuối>
  - Lệnh này thực hiện 3 việc:
    - Tạo branch `feature-login` ở local
    - Lấy trạng thái code từ `origin/feature-login`
    - Thiết lập upstream giữa local `login` và remote `origin/feature-login`
- Sau khi đã có branch ở local và upstream chỉ cần:
  - `git pull`: lấy code mới nhất về
  - `git add .`
  - `git commit -m "update"`
  - `git push`

### 5. Trường hợp 5: Nhiều người cùng sửa một file (học sau)

- `git push origin --delete test` xóa trực tiếp test branch trên remote, local vẫn còn ko ảnh hướng

# Ngày 14/11/2005 Bùi Thành Nam học tiếp github <"làm đi có đường hướng rồi, chỉ làm thôi, đừng có nghĩ nhiều">
  1. Bài 3.4 git fetch - tải về thông tin mới chưa gộp
    ```bash
      git fetch
    ```