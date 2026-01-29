✈️ AirProject — Airline Reservation Web (Servlet/JSP + Oracle)

**Java Servlet/JSP + Oracle DB**로 구현한 항공 예약 웹 애플리케이션입니다.  
사용자는 **회원가입/로그인 → 예약 생성 → 내 예약 조회/취소** 흐름을 이용할 수 있고,  
관리자는 **회원/예약 관리 기능**을 수행할 수 있습니다.

---

📌 Demo Flow (시연 흐름)
- **회원가입 → 로그인**
- **예약 생성**(편도/왕복, 인원 수 입력)
- **내 예약 조회**(목록)
- **예약 취소**
- **예약 조회(문의)**: 예약번호 + 아이디 + 출발일로 단건 조회
- **관리자(admin)**: 회원 목록/수정/삭제, 예약 목록/삭제

---

🧩 주요 기능

- **사용자**
  - **회원가입/로그인**
  - **예약 생성**: 편도/왕복(`TRIP_TYPE`), 출발/도착, 출발일/복귀일, 인원(성인/소아/유아)
  - **내 예약 목록 조회** / **예약 취소**
  - **예약 조회(문의)**: `RES_ID` + `USER_ID` + `DEPART_DATE`로 조회
  - **프로필 수정** / **회원 탈퇴**

**관리자**
  - **관리자 판별**: 로그인 `userid`가 **`admin`** 이면 `isAdmin=true`
  - **회원 관리**: 목록 조회 / 회원 정보 수정 / 회원 삭제(단, `admin` 삭제 불가)
  - **예약 관리**: 목록 조회 / 예약 삭제

---

⚙️ Tech Stack
- **Backend**: Java, Jakarta Servlet
- **Frontend**: JSP, CSS
- **DB**: Oracle (XE 기준)
- **WAS**: **Tomcat 10+ 권장** (코드가 `jakarta.servlet.*` 기반)
- **IDE**: Eclipse (Dynamic Web Project)

---
## 📂 프로젝트 구조

```text
AirProject-main
├─ .classpath
├─ .project
├─ .settings/
│  └─ (Eclipse 설정 파일들)
│
├─ AirProject.sql              # Oracle 스키마 / 쿼리
├─ README.md                   # 프로젝트 설명
│
├─ build/
│  └─ classes/
│
├─ src/
│  └─ main/
│     ├─ java/
│     │  ├─ dao/
│     │  │  └─ MemberDAO.java
│     │  ├─ servlet/
│     │  │  ├─ Member.java
│     │  │  ├─ Reservation.java
│     │  │  ├─ LoginServlet.java
│     │  │  ├─ LogoutServlet.java
│     │  │  ├─ RegisterServlet.java
│     │  │  ├─ EditUserServlet.java
│     │  │  ├─ UpdateProfileServlet.java
│     │  │  ├─ DeleteAccountServlet.java
│     │  │  ├─ DeleteUserServlet.java
│     │  │  ├─ ReservationServlet1.java
│     │  │  ├─ MyReservationsServlet.java
│     │  │  ├─ ManageReservationsServlet.java
│     │  │  ├─ DeleteReservationServlet.java
│     │  │  ├─ cancelReservation.java
│     │  │  ├─ ManageUsersServlet.java
│     │  │  └─ InquiryServlet.java
│     │  └─ util/
│     │     └─ DBUtil.java
│     └─ webapp/
│        ├─ login.jsp
│        ├─ signup.jsp
│        ├─ main.jsp
│        ├─ AdminDashboard.jsp
│        ├─ manageUsers.jsp
│        ├─ manageReservations.jsp
│        ├─ my_reservations.jsp
│        ├─ inquiryForm.jsp
│        ├─ flight.jsp
│        ├─ reservation_success.jsp
│        ├─ style.css
│        ├─ main.css
│        ├─ flight.css
│        └─ WEB-INF/
│           ├─ web.xml
│           └─ lib/
│              ├─ ojdbc11.jar
│              └─ jakarta.servlet.jsp.jstl-3.0.0.jar



실행 방법 (Eclipse + Tomcat)
1) Oracle 준비
Oracle XE 실행
위 DDL 실행(MEMBER, RESERVATION, RESERVATION_SEQ 생성)

3) Eclipse 프로젝트 로드
프로젝트 Import (Dynamic Web Project 형태)
Server(Runtime)에 Tomcat 10+ 등록
4) JDBC 드라이버
Oracle JDBC 드라이버(ojdbc)가 필요함.

5) 실행
Eclipse → Run on Server
접속: http://localhost:8080/<context>/main.jsp
