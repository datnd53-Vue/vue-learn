# Câu hỏi: 

## question 1. Tại sao Vue cần chia ra Doc và Api 

<img width="2048" height="1207" alt="image" src="https://github.com/user-attachments/assets/d0fb0d6a-e0a0-4334-8cfd-94c597ec821b" />


<img width="2048" height="1207" alt="image" src="https://github.com/user-attachments/assets/b3c67d25-f6a4-431a-990e-483dc1b46f95" />

#### => Docs là bản đồ còn API là từ điển. (Lập trình là hiểu tư duy trước, thuộc api sau)


- Nếu bạn vào phần Introduction trong Docs, Vue đang kể một câu chuyện: Vue là gì, tư duy ra sao, component hoạt động thế nào, reactivity là cái quái gì. Nó dắt bạn đi từ tư tưởng → mô hình → cách dùng. Đây là hướng “hiểu để làm”.

- Còn API thì không kể chuyện. API nói thẳng như kỹ sư công trường: (api giúp developer kết nối với Vue)
`data(): object`
`watch(source, callback, options)`
Nó là đặc tả kỹ thuật. Không màu mè. Không dẫn dắt. Chỉ định nghĩa chính xác từng option, từng tham số, từng kiểu trả về.

**Vì sao phải tách?**

- Thứ nhất: mục đích khác nhau.
Docs dạy tư duy. API tra cứu chi tiết.

- Thứ hai: người đọc khác nhau.
Người mới cần Docs.
Người đã biết Vue nhưng quên tham số của `watch` thì nhảy thẳng vào API.

- Thứ ba: tránh nhiễu nhận thức.
Nếu trộn hết lại, bạn sẽ vừa đọc “Reactivity Fundamentals” vừa bị đập vào mặt bằng interface TypeScript dài 20 dòng. Não sẽ cháy.

- Thứ tư: tính chính xác.
API cần cực kỳ chặt chẽ và cập nhật theo version. Docs có thể diễn giải mềm hơn. Hai thứ có vòng đời chỉnh sửa khác nhau.

Nói cách khác:
Docs trả lời “Tại sao và dùng thế nào?”
API trả lời “Cụ thể từng dòng nghĩa là gì?”

**chú ý**
- Vue không mở ruột gan cho bạn xem. Nó chỉ cho bạn một số cửa chính thức để đi vào. Những cửa đó chính là API.
- Interface là khái niệm chung & API là một loại interface.


## Question 2. Giải thích chi tiết hơn về Api 

***chú ý**
- ``COMPOSITION API`` và ``OPTIONS API`` mục đích là giống nhau, nó chỉ khác cách viết (dự án hiện tại đang là Vue 2 sử dụng OPTIONS API)
=> có thể bỏ qua ``COMPOSITION API`` để tập trung vào ``OPTIONS API``

### 1. GLOBAL API

=> Đây là những thứ dùng ở cấp ứng dụng, không phải bên trong một component.

**Application**
Mấy thứ như `createApp()`, `app.mount()`, `app.use()`…
Nó khởi tạo và cấu hình toàn bộ app.
Nghĩ nó như bật máy, cài plugin, rồi mới bắt đầu chạy.

**General**
Các utility toàn cục như `nextTick()`, `defineComponent()`…
Không thuộc riêng reactivity hay component nào, nhưng dùng khắp nơi.

### 2. COMPOSITION API

=> Đây là “cách viết Vue kiểu mới” trong Vue 3. Tập trung vào logic hơn là cấu trúc option.

**setup()**

Điểm vào chính của ``Composition API``.
Tất cả ``reactive state, logic, lifecycle hook`` mới đều khởi phát từ đây.

**Reactivity: Core**

Mấy hàm cốt lõi như `ref()`, `reactive()`, `computed()`, `effect()`…
Đây là trái tim của Vue 3. Proxy, dependency tracking, update DOM đều bắt đầu từ đây.

**Reactivity: Utilities**

Các helper như `toRefs()`, `isRef()`, `unref()`…
Không tạo reactivity mới, nhưng giúp thao tác với nó gọn hơn.

**Reactivity: Advanced**

`shallowRef()`, `markRaw()`, `customRef()`…
Dành cho người cần kiểm soát sâu về hiệu năng hoặc hành vi reactive.

**Lifecycle Hooks**

`onMounted()`, `onUpdated()`…
Phiên bản Composition của vòng đời component.

**Dependency Injection**

`provide()` và `inject()`
Truyền dữ liệu xuyên nhiều tầng component mà không cần props lòng vòng.

**Helpers**
Mấy hàm hỗ trợ khác như `useSlots()`, `useAttrs()`…
Công cụ phụ trợ khi viết component phức tạp.


### 3. OPTIONS API

Đây là cách viết truyền thống của Vue 2. Vue 3 vẫn giữ để tương thích.

**Options: State**

`data`, `props`, `computed`, `methods`, `watch`
Định nghĩa state và logic theo kiểu object config.

**Options: Rendering**

`render()`, `template`
Kiểm soát cách component hiển thị.

**Options: Lifecycle**

`mounted`, `created`, `beforeUnmount`…
Vòng đời kiểu cũ.

**Options: Composition**

Cho phép trộn Composition API vào Options API.

**Options: Misc**

Mấy config khác như `name`, `components`, `directives`.

**Component Instance**

Mô tả `this` trong component có gì bên trong.
Cái này dành cho ai muốn hiểu nội bộ sâu hơn.


### 4. BUILT-INS

Những thứ Vue cung cấp sẵn.

**Directives**

`v-if`, `v-for`, `v-model`, `v-bind`…
Cú pháp đặc biệt trong template.

**Components**

Component built-in như `<Teleport>`, `<Suspense>`, `<KeepAlive>`…

**Special Elements**

`<component>`, `<slot>`…
Phần tử đặc biệt do Vue xử lý riêng.

**Special Attributes**

`key`, `ref`, `is`…
Thuộc tính đặc biệt ảnh hưởng đến cơ chế render.


### 5. SINGLE-FILE COMPONENT

Syntax Specification
Cấu trúc file `.vue` gồm `<template>`, `<script>`, `<style>` hoạt động ra sao.

``<script setup> ``
Cú pháp sugar mới để viết Composition API gọn hơn.



  
### Tại sao phải chia vậy?

Vì Vue không chỉ là một thư viện nhỏ. Nó là một hệ sinh thái runtime:

- Cấp ứng dụng
- Cấp component
- Cấp reactivity engine
- Cấp template compiler

Nếu không chia theo trách nhiệm, dev sẽ lẫn lộn:

“Cái này dùng trong setup hay ngoài app?”  
“Cái này là runtime hay compile-time?”  
“Cái này thuộc Options hay Composition?”

Thiết kế tài liệu phản ánh thiết kế kiến trúc.

Framework trưởng thành không phải cái có nhiều tính năng.  
Mà là cái có cấu trúc rõ ràng.


