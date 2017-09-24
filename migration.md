## Sử dụng migration để tạo table CSDL

Migration giúp quản lý/theo dõi các hoạt động truy xuất, thêm xóa sửa csdl.
Nhập lệnh vào terminal, tên migration sẽ là hành động mà ta muốn thực hiện trên csdl, ở đây ta muốn tạo table mới tên là tasks

`php artisan make:migration create_tasks_table`

Sau khi nhập lệnh, một file migration mới sẽ được tạo trong đường dẫn `database/migrations`. Tuy nhiên, file này chưa chứa bất kì function nào để tạo bảng. php artisan có hỗ trợ sẵn một tùy chọn giúp tạo ra ngay function tạo bảng khi tạo migration.

`php artisan make:migration create_tasks_table --create=tasks`
Sau khi nhập xong lệnh, ta sẽ có một file migration mới với sẵn hàm tạo bảng _tasks_

```php
public function up()
{
  // namespace Shema giúp tạo bảng 'tasks' với sẵn 2 trường là 'id' và 'timestamps'
  Schema::create('tasks', function (Blueprint $table) {
    $table->increments('id');
    $table->timestamps();
  });
}
```
Sau khi tạo xong file migration, ta sẽ tiến hành migrate để xác nhận các thay đổi này vào csdl.
Nhập vào terminal: ` php artisan migrate` để xác nhận thay đổi.

Nếu có sai sót gì trong file migration. Các bạn chỉ cần sửa lại file migration, sau đó nhập lệnh `php artisan migrate:refresh`

Sau khi migrate xong, trong CSDL đã có bảng tasks. Để truy xuất csdl, ta có thể sử dụng các hàm DB của laravel ở đây [Cheatsheet](http://cheats.jesse-obrien.ca/#db)