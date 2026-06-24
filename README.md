# 🎓 Hệ thống Quản lý Khóa học — Giảng viên (Web)

> **Phiên bản:** 1.0.0  
> **Công nghệ:** React 18 + Vite 7 + Ant Design 5

---

## 🌐 Hệ thống liên quan

Dự án này là một phần trong **hệ thống quản lý khóa học trực tuyến** bao gồm 3 repo:

| Thành phần | Mô tả | Link |
|---|---|---|
| 🌐 **Instructor Web** | Giao diện web dành cho giảng viên quản lý khóa học | [github.com/linh404/instructor_web](https://github.com/linh404/instructor_web) |
| ⚙️ **Backend API** | REST API server xử lý logic nghiệp vụ, database | [github.com/holyBeastt/android_basic_app_server](https://github.com/holyBeastt/android_basic_app_server) |
| 📱 **App (Mobile)** | Ứng dụng di động cho học viên (Flutter) | [github.com/holyBeastt/flutter_basic_app](https://github.com/holyBeastt/flutter_basic_app) |

> **Luồng hoạt động:**  
> `Instructor Web (React)` ← API → `Backend Server (Node.js)` ← DB → `Database`  
> `Mobile App (Flutter)` ← API → `Backend Server (Node.js)` ← DB → `Database`

---

## 📋 Mục lục

- [Tổng quan](#-tổng-quan)
- [Tính năng chính](#-tính-năng-chính)
- [Công nghệ sử dụng](#-công-nghệ-sử-dụng)
- [Cấu trúc dự án](#-cấu-trúc-dự-án)
- [Hướng dẫn cài đặt](#-hướng-dẫn-cài-đặt)
- [Kiến trúc hệ thống](#-kiến-trúc-hệ-thống)
- [API Endpoints](#-api-endpoints)
- [State Management](#-state-management)
- [Routing](#-routing)
- [Giao diện người dùng](#-giao-diện-người-dùng)
- [Đóng góp](#-đóng-góp)
- [Giấy phép](#-giấy-phép)

---

## 🎯 Tổng quan

**Instructor Web** là một ứng dụng web **Single Page Application (SPA)** được xây dựng bằng **React** và **Vite**, phục vụ cho việc quản lý khóa học trực tuyến dành riêng cho giảng viên. Ứng dụng cho phép giảng viên:

- Tạo, chỉnh sửa, xóa khóa học
- Quản lý cấu trúc nội dung khóa học dạng cây (Course → Sections → Lessons / Quizzes → Questions)
- Xem dashboard thống kê doanh thu, số lượng khóa học, học viên
- Quản lý thông tin cá nhân

Ứng dụng giao tiếp với backend REST API qua **Axios**, sử dụng **Zustand** để quản lý state, và **Ant Design 5** làm UI component library.

---

## ✨ Tính năng chính

### 🔐 Authentication
- Đăng nhập với JWT token
- Tự động đính kèm token vào tất cả request
- Xử lý hết hạn token (redirect về trang login)
- Route bảo vệ (ProtectedRoute) yêu cầu xác thực

### 📚 Quản lý Khóa học
- **Danh sách khóa học** với phân trang, tìm kiếm, sắp xếp
- **Tạo khóa học mới** với form nhập liệu chi tiết (tiêu đề, giá, level, mô tả, thumbnail, ...)
- **Chỉnh sửa khóa học** qua giao diện tabs:
  - **Tab Course Info**: Thông tin chung của khóa học
  - **Tab Course Content**: Quản lý nội dung qua cây thư mục
- **Xóa khóa học** với xác nhận

### 🏗️ Quản lý Nội dung (Tree Structure)
Khóa học được tổ chức theo cấu trúc phân cấp 4 cấp:

```
📦 Course
 ┣ 📂 Section 1
 ┃ ┣ 📄 Lesson 1.1
 ┃ ┣ 📄 Lesson 1.2
 ┃ ┗ 📝 Quiz 1.1
 ┃     ┗ ❓ Question 1
 ┃     ┗ ❓ Question 2
 ┗ 📂 Section 2
   ┗ 📄 Lesson 2.1
```

- **Sections**: Nhóm các bài học theo chủ đề
- **Lessons**: Bài học với nội dung rich text (sử dụng React-Quill)
- **Quizzes**: Bài kiểm tra với câu hỏi trắc nghiệm
- **Questions**: Câu hỏi trong quiz (hỗ trợ nhiều đáp án, chọn đáp án đúng)

### 📊 Dashboard
- Thống kê tổng quan: doanh thu, số khóa học, số học viên, số bài học
- Biểu đồ trực quan (tích hợp Ant Design Charts)

### 👤 Quản lý Hồ sơ
- Xem và cập nhật thông tin cá nhân
- Đổi avatar, bio
- Đổi mật khẩu

---

## 🛠️ Công nghệ sử dụng

### Core
| Công nghệ | Phiên bản | Mục đích |
|---|---|---|
| **React** | ^18.3.1 | UI Library |
| **Vite** | ^7.3.5 | Build tool & Dev server |
| **Ant Design** | ^5.29.3 | UI Component Library |
| **React Router** | ^7.18.0 | Quản lý routing |
| **Zustand** | ^5.0.4 | State management |
| **Axios** | ^1.9.0 | HTTP client |

### UI & Hỗ trợ
| Công nghệ | Phiên bản | Mục đích |
|---|---|---|
| **React-Quill** | ^2.0.0 | Rich text editor cho nội dung bài học |
| **Styled Components** | ^6.1.17 | CSS-in-JS styling |
| **@ant-design/icons** | ^5.6.1 | Icon set |
| **Ant Design Charts** | ^2.1.3 | Biểu đồ thống kê |

### Development
| Công nghệ | Phiên bản | Mục đích |
|---|---|---|
| **ESLint** | ^9.25.1 | Linting |
| **@vitejs/plugin-react** | ^4.4.1 | React support cho Vite |
| **Vitest** | ^3.1.2 | Unit testing |
| **@testing-library/react** | ^16.3.0 | React testing utilities |

---

## 📁 Cấu trúc dự án

```
instructor_web/
│
├── .env                          # Biến môi trường
├── .gitignore
├── eslint.config.js              # ESLint flat config
├── index.html                    # HTML entry point
├── package.json                  # Dependencies & scripts
├── vite.config.js                # Vite configuration
├── README.md
│
├── public/
│   └── vite.svg
│
└── src/
    ├── main.jsx                  # Entry point React
    ├── App.jsx                   # Root component + Routes + Theme
    ├── App.css                   # Global styles cho App
    ├── index.css                 # Global CSS reset & base styles
    │
    ├── components/               # Components tái sử dụng
    │   ├── Layout/
    │   │   └── MainLayout.jsx    # Layout chính (Header + Sider + Content)
    │   │
    │   ├── Forms/
    │   │   ├── CourseForm.jsx        # Form tạo/sửa khóa học
    │   │   ├── DetailForm.jsx        # Form chi tiết (khóa học)
    │   │   ├── LessonForm.jsx        # Form tạo/sửa bài học
    │   │   ├── QuizForm.jsx          # Form tạo/sửa quiz
    │   │   ├── SectionForm.jsx       # Form tạo/sửa section
    │   │   └── UserProfileForm.jsx   # Form hồ sơ người dùng
    │   │
    │   ├── TreeView/
    │   │   └── CourseTreeView.jsx    # Cây nội dung khóa học
    │   │
    │   ├── ErrorBoundary.jsx         # Bắt lỗi React
    │   ├── NotificationManager.jsx   # Quản lý thông báo toàn cục
    │   └── ProtectedRoute.jsx        # Route bảo vệ (yêu cầu đăng nhập)
    │
    ├── pages/                    # Page components (tương ứng với routes)
    │   ├── Login.jsx / Login.css     # Trang đăng nhập
    │   ├── Dashboard.jsx             # Trang tổng quan / thống kê
    │   ├── CourseManagement.jsx      # Quản lý danh sách khóa học
    │   ├── CourseDetail.jsx          # Chi tiết khóa học
    │   ├── EditCourse.jsx            # Chỉnh sửa khóa học (giao diện tabs)
    │   └── ProfilePage.jsx           # Hồ sơ người dùng
    │
    ├── services/                 # API services
    │   ├── api.js                    # Axios client + tất cả API calls
    │   └── authService.js            # Authentication service
    │
    ├── store/                    # State management
    │   └── courseStore.js            # Zustand store cho course + UI state
    │
    └── utils/                    # Utility functions
        ├── formatters.js            # Format số, ngày tháng, ...
        └── validation.js            # Validation rules cho forms
```

---

## 🚀 Hướng dẫn cài đặt

### Yêu cầu hệ thống

- **Node.js** >= 18.x
- **npm** >= 9.x hoặc **pnpm** >= 8.x

### Cài đặt

```bash
# Clone repository
git clone https://github.com/linh404/instructor_web.git
cd instructor_web

# Cài đặt dependencies (dùng pnpm — khuyến nghị)
pnpm install

# Hoặc dùng npm
npm install
```

### Cấu hình môi trường

Tạo file `.env` tại thư mục gốc với nội dung:

```env
VITE_API_BASE_URL=http://localhost:3000/api/instructor
```

### Chạy ứng dụng

```bash
# Development mode (mặc định port 3001, tự động mở trình duyệt)
pnpm run dev

# Hoặc dùng npm
npm run dev
```

### Build production

```bash
pnpm run build
npm run build
```

Output sẽ được tạo trong thư mục `dist/`.

### Tài khoản mẫu

Ứng dụng yêu cầu tài khoản giảng viên (instructor role) để truy cập. Vui lòng đăng nhập với tài khoản có quyền giảng viên.

---

## 🏛️ Kiến trúc hệ thống

### Client Architecture Pattern

Ứng dụng sử dụng kiến trúc **layered architecture**:

```
┌─────────────────────────────────────┐
│            Pages (Routes)           │
│    Dashboard / CourseManagement     │
└──────────────┬──────────────────────┘
               │ uses
┌──────────────▼──────────────────────┐
│        Business Components          │
│  EditCourse / CourseDetail / Forms  │
└──────────────┬──────────────────────┘
               │ uses
┌──────────────▼──────────────────────┐
│     Shared / Reusable Components    │
│  Layout / TreeView / ProtectedRoute │
└──────────────┬──────────────────────┘
               │ uses
┌──────────────▼──────────────────────┐
│         State Management            │
│  Zustand Store (courseStore.js)     │
└──────────────┬──────────────────────┘
               │ calls
┌──────────────▼──────────────────────┐
│         API Services                │
│  Axios Client (api.js)              │
└──────────────┬──────────────────────┘
               │ HTTP
┌──────────────▼──────────────────────┐
│       Backend REST API              │
│   http://localhost:3000/api/...     │
└─────────────────────────────────────┘
```

### Data Flow

1. **Pages** gọi **Zustand actions** từ `courseStore.js`
2. **Actions** gọi **API services** (`api.js`) thông qua Axios
3. Axios tự động gắn JWT token qua interceptor
4. Response trả về → cập nhật state trong store
5. React components tự động re-render do Zustand subscription

### Theme Configuration (`App.jsx`)

Ứng dụng sử dụng **Ant Design ConfigProvider** với theme tùy chỉnh:

- **Primary Color**: Indigo (`#6366f1`) — hiện đại
- **Border Radius**: 12px (components), 8px (buttons, inputs)
- **Font**: Hệ thống (SF Pro, Segoe UI, ...)
- **Box Shadow**: Soft shadow hiện đại
- Hỗ trợ tiếng Việt qua locale `viVN`

---

## 🌐 API Endpoints

Tất cả API đều được gọi thông qua Axios instance với base URL mặc định:  
`http://localhost:3000/api/instructor`

### Authentication
| Method | Endpoint | Mô tả |
|---|---|---|
| POST | `/auth/login` | Đăng nhập |

### Courses
| Method | Endpoint | Mô tả |
|---|---|---|
| GET | `/courses` | Lấy danh sách khóa học (có phân trang, search, sort) |
| POST | `/courses` | Tạo khóa học mới |
| GET | `/courses/:id` | Chi tiết khóa học |
| PUT | `/courses/:id` | Cập nhật khóa học |
| DELETE | `/courses/:id` | Xóa khóa học |
| GET | `/courses/revenue-stats` | Thống kê doanh thu |

### Sections
| Method | Endpoint | Mô tả |
|---|---|---|
| GET | `/sections?course_id=` | Lấy sections của khóa học |
| POST | `/courses/:id/sections` | Thêm section mới |
| PUT | `/sections/:id` | Cập nhật section |
| DELETE | `/sections/:id` | Xóa section |

### Lessons
| Method | Endpoint | Mô tả |
|---|---|---|
| GET | `/lessons?section_id=` | Lấy lessons của section |
| POST | `/sections/:id/lessons` | Thêm lesson mới |
| PUT | `/lessons/:id` | Cập nhật lesson |
| DELETE | `/lessons/:id` | Xóa lesson |

### Quizzes
| Method | Endpoint | Mô tả |
|---|---|---|
| GET | `/quizzes?lesson_id=` | Lấy quizzes của lesson |
| POST | `/lessons/:id/quizzes` | Thêm quiz mới |
| PUT | `/quizzes/:id` | Cập nhật quiz |
| DELETE | `/quizzes/:id` | Xóa quiz |

### Questions
| Method | Endpoint | Mô tả |
|---|---|---|
| GET | `/questions?quiz_id=` | Lấy questions của quiz |
| POST | `/quizzes/:id/questions` | Thêm question mới |
| PUT | `/questions/:id` | Cập nhật question |
| DELETE | `/questions/:id` | Xóa question |

### Checkpoints (Lesson Checkpoints)
| Method | Endpoint | Mô tả |
|---|---|---|
| GET | `/lesson-checkpoints` | Lấy danh sách checkpoints |
| POST | `/lesson-checkpoints` | Tạo checkpoint mới |
| PUT | `/lesson-checkpoints/:id` | Cập nhật checkpoint |
| DELETE | `/lesson-checkpoints/:id` | Xóa checkpoint |

### User
| Method | Endpoint | Mô tả |
|---|---|---|
| GET | `/:id/get-user-info` | Lấy thông tin người dùng |
| PUT | `/update/:id` | Cập nhật thông tin người dùng |

---

## 🗃️ State Management

Ứng dụng sử dụng **Zustand** với một store duy nhất (`courseStore.js`).

### State
| State | Kiểu | Mô tả |
|---|---|---|
| `courses` | Array | Danh sách khóa học |
| `totalCourses` | Number | Tổng số khóa học |
| `currentCourse` | Object | Khóa học đang được chọn/chỉnh sửa |
| `courseTree` | Object | Cấu trúc cây nội dung khóa học |
| `selectedNode` | Object | Node đang được chọn trong tree |
| `expandedKeys` | Array | Các node đang mở rộng |
| `selectedKeys` | Array | Các node đang được chọn |
| `loadingStates` | Object | Trạng thái loading cho từng resource |
| `notifications` | Array | Hàng đợi thông báo |
| `errors` | Object | Lỗi theo resource key |
| `history` | Array | Lịch sử undo/redo |
| `historyIndex` | Number | Vị trí hiện tại trong lịch sử |

### Actions chính
| Action | Mô tả |
|---|---|
| `fetchCourses(params)` | Lấy danh sách khóa học |
| `fetchCourse(id)` | Lấy chi tiết khóa học |
| `createCourse(data)` | Tạo khóa học mới |
| `updateCourse(id, data)` | Cập nhật khóa học |
| `deleteCourse(id)` | Xóa khóa học |
| `fetchSections(courseId)` | Lấy sections |
| `createSection(courseId, data)` | Thêm section |
| `updateSection(id, data)` | Cập nhật section |
| `deleteSection(id)` | Xóa section |
| `fetchLessons(sectionId)` | Lấy lessons |
| `createLesson(sectionId, data)` | Thêm lesson |
| `updateLesson(id, data)` | Cập nhật lesson |
| `deleteLesson(id)` | Xóa lesson |
| `fetchQuizzes(lessonId)` | Lấy quizzes |
| `createQuiz(lessonId, data)` | Thêm quiz |
| `updateQuiz(id, data)` | Cập nhật quiz |
| `deleteQuiz(id)` | Xóa quiz |
| `fetchQuestions(quizId)` | Lấy questions |
| `createQuestion(quizId, data)` | Thêm question |
| `updateQuestion(id, data)` | Cập nhật question |
| `deleteQuestion(id)` | Xóa question |

### Undo/Redo
Store hỗ trợ undo/redo cơ bản:
- `saveToHistory()` — Lưu snapshot hiện tại
- `undo()` — Quay lại trạng thái trước
- `redo()` — Tiến tới trạng thái tiếp theo
- `canUndo()` / `canRedo()` — Kiểm tra khả năng undo/redo

### Selectors (Optimize re-renders)
```js
useCoursesSelector()         // Chỉ re-render khi courses thay đổi
useCurrentCourseSelector()   // Chỉ re-render khi currentCourse thay đổi
useCourseTreeSelector()      // Chỉ re-render khi courseTree thay đổi
useSelectedNodeSelector()    // Chỉ re-render khi selectedNode thay đổi
useLoadingSelector()         // Chỉ re-render khi loadingStates thay đổi
```

---

## 🧭 Routing

Định nghĩa routes trong `App.jsx` sử dụng **React Router v7**:

| Path | Component | Protected | Mô tả |
|---|---|---|---|
| `/login` | Login | ❌ | Trang đăng nhập |
| `/` | Dashboard | ✅ | Trang tổng quan |
| `/courses` | CourseManagement | ✅ | Danh sách khóa học |
| `/courses/new` | CourseForm | ✅ | Tạo khóa học mới |
| `/courses/:id` | CourseDetail | ✅ | Chi tiết khóa học |
| `/courses/:id/edit` | CourseForm | ✅ | Chỉnh sửa khóa học |
| `/courses/:courseId/edit` | EditCourse | ✅ | Chỉnh sửa (legacy) |
| `/profile` | ProfilePage | ✅ | Hồ sơ người dùng |
| `/dashboard` | Redirect → / | ✅ | Redirect legacy |
| `*` | 404 Page | ✅ | Fallback |

Tất cả route (trừ `/login`) đều được bọc trong `ProtectedRoute` kiểm tra token hợp lệ.

---

## 🎨 Giao diện người dùng

### Layout
- **Header**: Logo + Menu điều hướng
- **Sider**: Sidebar với menu chính
- **Content**: Nội dung chính

### Theme
- **Modern Indigo**: Màu chủ đạo `#6366f1`
- **Border Radius**: Bo tròn 12px
- **Soft Shadow**: Shadow nhẹ cho cards, buttons
- **Responsive**: Thiết kế linh hoạt (có thể mở rộng)

### Trang chính

#### Dashboard
- Cards thống kê: Doanh thu, khóa học, học viên, bài học
- Biểu đồ trực quan

#### Course Management
- Bảng danh sách khóa học với filter/sort/search
- Modal/Create form cho thao tác CRUD
- Phân trang

#### Edit Course
- Giao diện tabs (Course Info / Course Content)
- **Course Info**: Form chỉnh sửa thông tin
- **Course Content**: 
  - TreeView hiển thị cấu trúc khóa học dạng cây
  - Click vào node để xem/sửa chi tiết
  - Form động thay đổi theo loại node (Section/Lesson/Quiz/Question)
  - Hỗ trợ rich text editor cho nội dung bài học

---

## 🤝 Đóng góp

Mọi đóng góp đều được chào đón! Vui lòng:

1. Fork repository
2. Tạo branch mới (`git checkout -b feature/ten-tinh-nang`)
3. Commit thay đổi (`git commit -m 'feat: thêm tính năng mới'`)
4. Push lên branch (`git push origin feature/ten-tinh-nang`)
5. Tạo Pull Request

### Coding Standards
- Sử dụng ESLint với cấu hình có sẵn
- Tuân thủ quy tắc đặt tên: camelCase cho variables/functions, PascalCase cho components
- JSDoc comments cho functions phức tạp

---

## 📄 Giấy phép

Dự án này được phát triển cho mục đích quản lý khóa học trực tuyến.

---

<p align="center">Made with ❤️ for instructors</p>