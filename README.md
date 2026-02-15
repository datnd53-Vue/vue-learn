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

## Chi tiết OPTIONS API


**Options: State**

`data`, `props`, `computed`, `methods`, `watch`
Định nghĩa state và logic theo kiểu object config.

### 1. `data()` là hàm trả về **state ban đầu** của component.

Nói gọn, **`data` trong Vue là cái “kho trạng thái ban đầu” của component**.

Nó là một function trả về **một object thuần (plain object)**. Vue lấy object đó và biến nó thành **reactive** – tức là khi dữ liệu thay đổi, giao diện tự cập nhật. Không cần gọi refresh, không cần thao tác DOM tay chân. Vue lo.
**`data()` phải trả về một object đơn giản. Ví dụ:**

```js
data() {
  return { a: 1 }
}
```

Sau khi component được tạo:

* `this.$data` chính là object đó.
* `this.a` thực chất là Vue proxy từ `this.$data.a`.

Nói dễ hiểu: Vue đứng giữa làm “phiên dịch viên”. Bạn gọi `this.a`, nó chuyển xuống `this.$data.a`.

**Tất cả các biến top-level phải khai báo sẵn trong `data()`.**

Đừng kiểu:

```js
this.b = 2 // tự nhiên mọc thêm sau này
```

Vue vẫn cho thêm, nhưng **không khuyến khích**. Vì hệ thống reactivity hoạt động tốt nhất khi nó biết trước toàn bộ cấu trúc state. Nếu chưa có giá trị thì cứ để:

```js
return {
  user: null,
  loading: false,
  error: undefined
}
```

Khai báo trước giống như vẽ sơ đồ nhà trước khi xây. Đừng xây thêm phòng sau khi đã đổ móng.

**Biến bắt đầu bằng `_` hoặc `$` sẽ không được proxy lên `this`.**

Ví dụ:

```js
return {
  _private: 123
}
```

Bạn phải truy cập bằng:

```js
this.$data._private
```

Vì `$` và `_` có thể trùng với hệ thống nội bộ của Vue. Vue giữ “khu vực kỹ thuật” riêng.

**Không nên trả về object có hành vi phức tạp như:**

* Browser API object
* Object có prototype riêng
* Class instance

`data()` chỉ nên chứa **state thuần túy**, không logic ẩn bên trong. State là dữ liệu. Hành vi là method. Phân biệt cho rõ ràng. Truyền thống phần mềm chuẩn mực là vậy.

**Đừng dùng arrow function nếu bạn cần `this`:**

```js
data: () => ({ a: 1 }) // this sẽ không phải component
```

Arrow function không có `this` riêng. Nó mượn từ scope ngoài. Nếu cần instance thì dùng function thường:

```js
data() {
  return { a: this.myProp }
}
```

Hoặc nếu bắt buộc dùng arrow, bạn có thể dùng tham số đầu tiên:

```js
data: (vm) => ({ a: vm.myProp })
```

***Vue bọc object bạn trả về bằng `Proxy`. Proxy là cơ chế của JavaScript cho phép “chặn” việc đọc/ghi dữ liệu. Khi bạn đổi `this.a = 5`, Proxy phát hiện ra và kích hoạt cập nhật UI.
Đây là reactive system. Nó giống như một hệ thần kinh nhỏ bên trong component. Động vào data là thần kinh bắn tín hiệu ra giao diện.***


### 2. props

=> thứ làm cho component không còn là cục đá vô tri, mà trở thành “đứa con biết nghe lời cha mẹ”.
 **props là dữ liệu truyền từ component cha xuống component con**. Một chiều. Từ trên xuống. Không cãi. Không đảo chiều. Truyền thống gia phong rõ ràng.

Về mặt type:

```ts
interface ComponentOptions {
  props?: string[] | Record<string, PropOptions>
}
```

**Có 2 cách khai báo.**

Cách đơn giản:

```js
props: ['title', 'count']
```

Cách nghiêm túc, có kiểm soát kiểu dữ liệu:

```js
props: {
  title: String,
  count: {
    type: Number,
    required: true,
    default: 0
  }
}
```

Vue sẽ kiểm tra type trong dev mode. Không phải TypeScript-level chặt chẽ, nhưng đủ để bắt lỗi ngớ ngẩn.


**Cơ chế hoạt động thế nào?**

Cha truyền xuống:

```html
<MyCard title="Hello" :count="5" />
```

Con nhận:

```js
export default {
  props: ['title', 'count'],
  created() {
    console.log(this.title) // "Hello"
  }
}
```

Vue proxy props giống như data. Bạn truy cập bằng `this.title`.

Nhưng có một luật thép: ***props là read-only trong component con.***

Bạn không được làm:

```js
this.title = 'Changed'
```

Vì props đại diện cho state của cha. Nếu con sửa, luồng dữ liệu rối tung như dây tai nghe bỏ túi quần.

Vue sẽ cảnh báo ngay.


**Nếu muốn chỉnh sửa giá trị ban đầu của prop?**

Cách đúng đắn là:

```js
props: ['initialValue'],
data() {
  return {
    localValue: this.initialValue
  }
}
```

Hoặc dùng computed.

Tư duy đúng là:
Prop = input
Data = state nội bộ
Emit = output

Component chuẩn mực giống một hàm thuần: nhận input, xử lý, phát output.


Một chi tiết thú vị: **props cũng reactive**.

Nếu cha thay đổi giá trị:

```js
this.count = 10
```

Con sẽ tự cập nhật lại. Không cần làm gì thêm. Vì Vue theo dõi dependency.

**Default value trong props object phải là function nếu là object hoặc array:**

Sai:

```js
default: []
```

Đúng:

```js
default: () => []
```

Lý do? Nếu không, tất cả instance sẽ dùng chung một array. Và rồi bạn có một bug nhìn như ma ám. Một instance sửa, instance khác tự đổi theo. Vì chúng đang dùng chung reference.

**Một tầng triết học nhỏ ở đây.**

Props giúp Vue giữ nguyên nguyên tắc:

***Single Source of Truth*** – chỉ có một nguồn dữ liệu gốc.
Cha quản lý state. Con hiển thị và tương tác.
Khi con muốn thay đổi gì đó, nó không sửa props. Nó emit event lên cha.

**Đó là cách hệ thống lớn giữ được sự minh bạch.**

Ví dụ emit:

```js
this.$emit('update-count', newValue)
```

Cha lắng nghe:

```html
<MyCard :count="count" @update-count="count = $event" />
```

Đây chính là pattern một chiều kinh điển. Rõ ràng. Kiểm soát được. Không drama.





### 3. **computed** – vũ khí tối thượng để xử lý dữ liệu một cách thanh lịch.

Nếu `data` là kho nguyên liệu thô,
thì `computed` là đầu bếp.

Computed là **giá trị được tính toán dựa trên reactive state**, và nó **được cache**.

**Khai báo kiểu cổ điển:**

```js
computed: {
  fullName() {
    return this.firstName + ' ' + this.lastName
  }
}
```

Dùng như biến bình thường:

```js
this.fullName
```

Không cần gọi như function. Vue tự tính khi cần.


Điểm ăn tiền: **caching (ghi nhớ kết quả)**.

Vue sẽ chỉ tính lại `fullName` khi `firstName` hoặc `lastName` thay đổi.

Nếu bạn gọi `this.fullName` 100 lần trong template, nó không tính 100 lần.
Nó nhớ kết quả. Thông minh. Không lãng phí CPU.

So với method:

```js
methods: {
  fullName() {
    return this.firstName + ' ' + this.lastName
  }
}
```

Mỗi lần render, method sẽ chạy lại. Không cache. Không thương lượng.

Computed giống như một bộ não biết ghi nhớ.
Method giống như người quên trước quên sau, mỗi lần đều làm lại từ đầu.


**Computed hoạt động nhờ hệ thống dependency tracking.**

Vue theo dõi xem trong computed bạn đọc những reactive property nào.
Nó tạo một “đường dây thần kinh” liên kết giữa chúng.

Khi dependency thay đổi → computed bị đánh dấu “dirty” → lần truy cập tiếp theo sẽ tính lại.

Cơ chế này dựa trên `Proxy` và effect tracking bên trong hệ reactivity của Vue.
Không ma thuật. Chỉ là JavaScript nâng cao.

**Computed cũng có thể có setter.**

```js
computed: {
  fullName: {
    get() {
      return this.firstName + ' ' + this.lastName
    },
    set(value) {
      const parts = value.split(' ')
      this.firstName = parts[0]
      this.lastName = parts[1]
    }
  }
}
```

Giờ bạn có thể:

```js
this.fullName = "John Doe"
```

Vue sẽ gọi setter.
Đây là cách v-model hoạt động phía sau hậu trường.


**Khi nào nên dùng computed?**

* Khi cần biến đổi dữ liệu để hiển thị
* Khi lọc list
* Khi tính toán dựa trên nhiều state
* Khi cần cache tự động

**Khi nào không nên?**

* Khi xử lý async
* Khi có side effect (gọi API, thay đổi state khác)

Computed phải thuần. Nó là toán học.
Input giống nhau → output giống nhau.

Nếu bạn nhét logic bẩn vào computed, bạn đang phá kiến trúc.

**Ví dụ thực tế:**

```js
computed: {
  activeUsers() {
    return this.users.filter(u => u.active)
  }
}
```

Mỗi khi `users` thay đổi → danh sách activeUsers cập nhật.

Bạn không phải quản lý thủ công. Vue lo.





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
