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

## 1. Cài đặt CSS-Loader và Style-Loader

- 2 thư viện này giúp webpack có thể tải file `.css` dưới dạng module. Chạy:

```
npm install css-loader style-loader --save-dev
```

## 2. Tạo webpack.config.js

- Tạo file `webpack.config.js` tại thư mục gốc của dự án với nội dung sau:

```javascript
const path = require("path");

module.exports = {
  entry: "./src/index.js", // Dẫn tới file index.js ta đã tạo
  output: {
    path: path.join(__dirname, "/build"), // Thư mục chứa file được build ra
    filename: "bundle.js", // Tên file được build ra
  },
  module: {
    rules: [
      {
        test: /\.js$/, // Sẽ sử dụng babel-loader cho những file .js
        exclude: /node_modules/, // Loại trừ thư mục node_modules
        use: ["babel-loader"],
      },
      {
        test: /\.css$/, // Sử dụng style-loader, css-loader cho file .css
        use: ["style-loader", "css-loader"],
      },
    ],
  },
  // Chứa các plugins sẽ cài đặt trong tương lai
  plugins: [],
};
```

- Lưu ý đặt file `webpack.config.js` ở thư mục gốc, ngang hàng với `package.json`

![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153e1bbaefe3.png)

## 3. Tạo file .babelrc

- File `.babelrc` dùng để cấu hình cho thư viện Babel.

> Lưu ý tên file bắt đầu bằng dấu `.`

- Tại thư mục gốc dự án tạo file `.babelrc` và thêm nội dung sau:

```javascript
{
  "presets": [
    "@babel/preset-env",
    "@babel/preset-react"
  ]
}
```

> Cài đặt này để cho Babel biết sử dụng `preset-env` và `preset-react` trong việc hỗ trợ chuyển đổi mã.

![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153e3d726261.png)

## 4. Thêm scripts cho dự án

- Tại `package.json` thêm nội dung sau:

```javascript
"scripts": {
  ...
  "start": "webpack --mode development --watch",
  "build": "webpack --mode production"
}
```

![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153e4d609bcb.png)

> Cấu hình `scripts` này để bạn có thể chạy lệnh tương ứng qua Terminal. Ví dụ: `npm start` sẽ chạy lệnh ở phần `start`, `npm run build` sẽ chạy lệnh ở phần `build`. Trừ `start` ra thì cần thêm `run`.

---

# Chạy dự án

## 1. Biên dịch code với Webpack

- Tại Ternimal hãy chạy:

```
npm start
```

> Lệnh này sẽ chạy `webpack --mode development --watch` mà ta đã cấu hình trong `package.json`, `--watch` để webpack sẽ luôn lắng nghe thay đổi, khi file thay đổi webpack sẽ thực hiện biên dịch nhé.

- Kết quả:

![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153e607aa5a2.png)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1. Có file mới được tạo ra trong `build/bundle.js` (vì đã cấu hình như vậy trong `webpack.config.js`)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2. Nội dung trong `build/bundle.js` chính là code của file `src/index.js` đã được Babel chuyển đổi, có thể mở ra để quan sát.

- Có rất nhiều code trong này vì nó bao gồm cả code của những thư viện đã import như: `react` và `react-dom`.

![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153e6b91f94f.png)

## 2. Chạy dự án với Live Server (VSCode)

- Phần này cần làm 2 việc:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1. Thêm thẻ script link tới file build/bundle.js

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2. Chạy dự án với Live Server

![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153e7dcc00c1.png)

- Thêm nội dung sau vào vị trí như ảnh mô tả ở trên:

```html
<script src="../build/bundle.js"></script>
```

- Sau đó chạy Live Server.

> Nhờ Live Server mà ta không cần F5 trang web.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1. Webpack khi được chạy sẽ lắng nghe thay đổi của file

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2. Khi file thay đổi Webpack sẽ biên dịch và update vào `build/bundle`.js

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;3. Website được chạy sẽ link file script từ `build/bundle.js`

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;4. Live Server chạy web và lắng nghe thay đổi của `build/bundle.js` để F5 lại trang

---

# Cài đặt html-webpack-plugin

- Tại sao phải cài thằng này làm gì? Ở phần trước ta phải tự đi thêm thằng này vào `index.html`

![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153ebf86311b.png)

- Làm như này khá thủ công, chúng ta có thể tự động hóa nó vì rõ ràng ta đã mất công cấu hình trong Webpack rồi mà.

![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153ec4689bac.png)

- Chính vì vậy `html-webpack-plugin` ra đời để giúp chúng ta “nhờ” Webpack sau khi build ra build/bundle.js thì thêm hộ chúng ta vào `public/index.html` luôn.

```
npm install html-webpack-plugin --save-dev
```

- Cài thành công sẽ trông như này:

![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153ed5c6adaa.png)

- Tiếp theo ta đi update cấu hình Webpack để thêm `html-webpack-plugin` vào dự án.

- Tại `webpack.config.js` hãy thêm:

```javascript
...
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  ...
  // Chứa các plugins sẽ cài đặt trong tương lai
  plugins: [
    new HtmlWebpackPlugin({
      template: "./public/index.html"
    })
  ]
};
```

- Làm đúng trông sẽ như sau:

![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153edf25bc79.png)

- Đi xóa bỏ phần khoanh đỏ khỏi file `public/index.html`:

![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153eedaeaae4.png)

- Nhấn `Ctrl + C` tại Terminal và chạy lại lệnh `npm start` để thấy kết quả!

![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153efd40fdf0.png)

> Thuộc tính `defer` trong thẻ script để báo với trình duyệt rằng hãy thực thi code Javascript sau khi HTML đã được parse xong. Điều này giúp đặt được thẻ script trên thẻ `head` mà code Javascript vẫn có thể truy cập được HTML DOM viết dưới `body`.

---

# Cài đặt webpack-dev-server

> Đây là bước cuối cùng của hướng dẫn này.

- Ở phần trước chúng ta vẫn sử dụng VSCode Live Server để chạy web, trong thực tế khi ta đã cài đặt Node và sử dụng Webpack thì ta sẽ không cần dùng tới Live Server. Bản thân Node có thể start được web server (máy chủ web) rồi, giờ ta sẽ đi cài thêm `webpack-dev-server` để có được một web server kết hợp được Webpack và Node nhé.

```
npm install webpack-dev-server --save-dev
```

- Sau khi cài đặt thành công:

![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153f23fe69b0.png)

- Sửa lại cấu hình scripts trong `package.json`:

```javascript
"scripts": {
  ...
  "start": "webpack-dev-server --mode development --open --hot",
  ...
}
```

- Làm đúng trông sẽ như sau:

![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153f1bc8dd55.png)

**_Tắt bỏ Live Server, nhấn `Ctrl + C` tại Terminal và chạy lại lệnh `npm start` để thấy kết quả!_**

---

# Thành quả

- Sau khi chạy `npm start`:

![img](https://cdn.fullstack.edu.vn/f8-learning/blog_posts/279/6153f3141edb9.png)
