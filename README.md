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

📁 프로젝트 구조 (핵심)
AirProject-main/
├─ src/main/java/
│  ├─ dao/              # MemberDAO (회원 CRUD/로그인)
│  ├─ servlet/          # 예약/관리/인증 관련 서블릿
│  └─ util/DBUtil.java  # DB 연결 유틸(회원 DAO가 사용)
└─ src/main/webapp/
   ├─ *.jsp, *.css
   └─ WEB-INF/
      ├─ web.xml
      └─ lib/           # (프로젝트에 포함된 jar들)


DB 코드
-- 회원
CREATE TABLE MEMBER (
  NAME   VARCHAR2(20) NOT NULL,
  USERID VARCHAR2(20) PRIMARY KEY,
  PWD    VARCHAR2(20) NOT NULL,
  PHONE  CHAR(20),
  EMAIL  VARCHAR2(20)
);

-- 예약

CREATE TABLE RESERVATION (
  RES_ID        NUMBER PRIMARY KEY,
  USER_ID       VARCHAR2(50),
  TRIP_TYPE     VARCHAR2(10), -- ONE_WAY or ROUND
  ORIGIN        VARCHAR2(10),
  DESTINATION   VARCHAR2(10),
  DEPART_DATE   DATE,
  RETURN_DATE   DATE,
  ADULT_COUNT   NUMBER,
  CHILD_COUNT   NUMBER,
  INFANT_COUNT  NUMBER,
  CREATED_AT    DATE DEFAULT SYSDATE
);

CREATE SEQUENCE RESERVATION_SEQ
START WITH 1
INCREMENT BY 1
NOCACHE;

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
