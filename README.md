# THÔNG BÁO ALERT
---
## Mô tả
-  Sử dụng để thông báo khi đăng nhập thành công, thất bại hoặc thay đổi trạng thái của một đối tượng

##  Cách sử dụng
-  Thêm element vào html (file muốn hiển thị các thông báo)
```html
    <!-- alert thông báo -->
    <div class="alert ">
        <!-- <div class="alert__item alert--success">
            <span>Tạo thành công !</span>
            <span close-alert>
                <i class="fa-solid fa-xmark"></i>
            </span>
        </div> -->
    </div>  
    <!-- hết alert thông báo -->
```
-  Thêm đoạn css vào file style.css hoặc có thể viết file riêng rồi link vào
```css
/* alert */
.alert {
    /* vị trí */
    position: fixed;
    top: 50px;
    right: 100px;

    /* thông báo đẩy */
    display: inline-flex;
    flex-direction: column;
    gap: 5px;
}

.alert__item {
    position: relative;
    display: inline-flex;
    width: 250px;
    padding: 8px 10px;
    font-size: 16px;
    border-radius: 5px;
}

.hideAlert {
    /* sử dụng keyframe animation */
    animation-name: alert-hidden;
    animation-duration: 0.5s; /** thời gian thực hiện */
    animation-fill-mode: both;
}
  
@keyframes alert-hidden {
    from {
      left: 0;
    }
    to {
      left: 200%;
      display: none;
    }
}

.alert__item [close-alert] {
    cursor: pointer;
    position: absolute;
    right: 5px;
    top: 8px;
}

.alert--success {
    background-color: #D4EDDA;
    color: #275724;
}

.alert--error {
    background-color: #F8D7DA;
    color: #721C24;
}

.alert--warning {
    background-color: #FFF3CD;
    color: #906404;
}
/* hết alert */
```
-  Import module show-alert này vào file js muốn thao tác
```javascript
/** @author Giang Trường */

// Thông báo alert
const alert = document.querySelector(".alert");
const showAlert = (content = null, state, time) => {

    if(content === null) return; // nếu không có nội dung thì return luôn

    const newAlertItem = document.createElement("div");

    newAlertItem.setAttribute("class", `alert__item alert--${state}`); 
    newAlertItem.innerHTML = `
        <span> ${content} ! </span>
        <span close-alert>
        <i class="fa-solid fa-xmark"></i>
        </span>
    `;
    alert.appendChild(newAlertItem);

    // khi nhấn vào nút close alert thì sẽ tắt alert đó
    const closeAlertItem = newAlertItem.querySelector("[close-alert");
    closeAlertItem.addEventListener("click", (event) => {
        newAlertItem.style.display = "none";
    });

    // sau TIME giây nếu không nhấn vào close alert thì nó sẽ tự tắt
    setTimeout(() => {
        // newAlertItem.style.display = "none";
        newAlertItem.classList.add("hideAlert");
    }, time);
    // return;
}
// Hết Thông báo alert

export default showAlert;
```

**Lưu ý**
```sh
  Các state trong file js tương ứng với "success", "warning", "error".
  Vì file css được viết chuẩn BEM. Các "success", "warning", "error" tương ứng với modify khi viết theo chuẩn BEM
```
