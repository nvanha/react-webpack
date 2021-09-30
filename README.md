# Bắt đầu

## 1. Cấu trúc dự án:

```php
react-webpack # thư mục gốc
    | src # thư mục chứa source code chính
        | components # thư mục chứa components
        | index.js # File khởi tạo, render App vào #root
    | public
        | index.html # HTML page, nơi chứa #root element
```

## 2. Khởi tạo dự án:

- **_File --> Add Folder to Workspace_**.

![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153cea07e4ad.png)

- Tạo thư mục mới tên là `react-webpack` sau đó click **_Add_**.

## 3. Mở cửa sổ Terminal

![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153cff03a78c.png)

- Khởi tạo dự án với Node:

```
npm init
```

> Gõ `npm init` vào Terminal sau đó nhấn phím `Enter` để chạy dòng lệnh.

- Kết quả trông như sau:

![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153d075949da.png)
![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153d1067cfd9.png)

- Sau khi khởi tạo dự án thành công sẽ thấy file `package.json` được tạo trong thư mục dự án.

![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153d1ac97279.png)

> `package.json` là file chứa thông tin dự án như: tên dự án, phiên bản, mô tả, các thư viện được sử dụng trong dự án, etc

## 4. Cài đặt webpack

- Chạy lệnh sau để cài đặt 2 thư viên là `webpack` và `webpack-cli`:

```
npm install webpack webpack-cli --save-dev
```

> `---save-dev` để đánh dấu 2 thư viện này chỉ dùng trong khi phát triển, khi dự án đẩy lên production sẽ không có các thư viện này.

- Sau khi lệnh trên chạy xong, `webpack` và `webpack-cli` sẽ được thêm vào `devDependencies`:

![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153d30c70fe1.png)

> `devDependencies` chứa các thư viện được cài đặt với flag `--save-dev`.

## 5. Cài đặt React và React-DOM

- Chạy lệnh sau:

```
npm install react react-dom --save
```

> `--save` để thêm các thư viện được cài vào phần `dependencies` trong `package.json`. Đây là các thư viện được sử dụng trong dự án, bao gồm cả development & production. Từ phiên bản NPM 5 trở đi thì `--save` được thêm vào mặc định, nếu bạn đang sử dụng NPM >= 5 thì có thể không cần `--save`.

- Sau khi cài đặt thành công:

![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153d48aac6dc.png)

## 6. Cài đặt Babel

- Chạy:

```
npm install @babel/core babel-loader @babel/preset-env @babel/preset-react --save-dev
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1. babel-core: Chuyển đổi ES6 về ES5

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2. babel-loader: Cho phép chuyển các files Javascript sử dụng Babel & Webpack

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;3. babel-preset-env: Cài đặt sẵn giúp bạn sử dụng Javascript mới nhất trên nhiều môi trường khác nhau (nhiều trình duyệt khác nhau). Gói này đơn giản là support truyển đổi ES6, ES7, ES8, ES… về ES5.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;4. babel-preset-react: Hỗ trợ chuyển đổi JSX về Javascript

- Sau khi cài đặt xong:

![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153d78206359.png)

## 7. Tạo index.html

- Tại thư mục gốc của dự án hãy tạo file public/index.html và thêm vào cấu trúc HTML mặc định như sau:

![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153de515c5c2.png)

> Thêm nhanh cấu trúc HTML mặc định với VSCode, gõ `!` và nhấn `Tab`.

- Tiếp theo, hãy tạo `#root` element:

![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153e0f670e43.png)

## 8. Tạo file index.js

- Tại thư mục gốc của dự án hãy tạo file `src/index.js` và thêm vào nội dung sau:

```javascript
import React from "react"; // nạp thư viện react
import ReactDOM from "react-dom"; // nạp thư viện react-dom

// Tạo component App
function App() {
  return (
    <div>
      <h1>Xin chào anh em F8!</h1>
    </div>
  );
}

// Render component App vào #root element
ReactDOM.render(<App />, document.getElementById("root"));
```

---

# Cấu hình webpack
