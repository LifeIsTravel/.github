# ✈️ LifeIsTravel
**합리적으로 여행하!** 
---

## 📌 프로젝트 소개

- **AWS 환경**에서 **Airflow Celery Executor**를 구축하여 데이터 파이프라인 설계  
- **항공권 가격 추이**를 한눈에 확인 가능  
- 예산 및 인기 장소 기반 **항공권 + 숙소 추천** 기능 제공  
- **정확한 여행 일정이 없어도** 편리한 항공권 검색 서비스 제공  
- **기상 조건**을 반영한 **항공편 지연 확률 예측 서비스** 제공  

---

## 👥 구성원 소개

<img src="https://github.com/user-attachments/assets/3091aef5-ae34-45ee-a9ca-e4474fda370a" width="800"/>

---

## 🗓️ 프로젝트 일정

<img src="https://github.com/user-attachments/assets/9891b090-bc71-48ff-b6dc-94e5a872e0cc" width="800"/>

---

## 🛠️ 기술 스택 및 프레임워크

<img src="https://github.com/user-attachments/assets/a6e9cb45-f28c-4dd1-984a-141f31466a33" width="800"/>

---

## 📊 대시보드

### 항공권 최저가 추이

- 출발일자와 도착일자 선택 시 **일별 항공권 최저가 추이** 정보 제공  
- **Snowflake View**로 자동 업데이트  

<div align="center">
  <img src="https://github.com/user-attachments/assets/1cfbfae7-b140-4bad-832e-e7971c5d6659" width="45%"/>
  <img src="https://github.com/user-attachments/assets/fe86f412-f50b-460f-bc9d-36677d3831e9" width="45%"/>
</div>

### 항공사별 운항 현황

- **일본 노선 운항 현황**과 2024년 운항 횟수 제공  
- **지연 및 결항 현황** 통계 제공  

<div align="center">
  <img src="https://github.com/user-attachments/assets/2e52b588-4cad-49de-8f88-e660d00d0cc5" width="45%"/>
  <img src="https://github.com/user-attachments/assets/6fdcc581-4f40-4a83-8e6f-c8ed88c22a64" width="45%"/>
</div>

---

## 🏗️ 전체 아키텍처

<img src="https://github.com/user-attachments/assets/971ce6aa-9172-431c-bcb2-ab3bd17f98f6" width="800"/>

---

## 🔄 Airflow 아키텍처

- **Celery Executor**와 **Auto Scaling Worker**로 구성하여 **분산 처리 환경** 구축  
- 다수의 DAG를 **동시 실행** 가능  

<img src="https://github.com/user-attachments/assets/38cc0453-694d-4eb6-a823-006bfd553611" width="800"/>

---

## 🌐 Django 아키텍처

- **Nginx(Public Subnet)** → **웹 서버(Django, Private Subnet)** 구조  
- **DNS 서버**와 연결을 통해 안정적인 서비스 제공  

<img src="https://github.com/user-attachments/assets/3660a037-0373-4471-8f61-3831c7c62ddd" width="800"/>

---
## 🔎 데이터 파이프라인

1. **데이터 수집:**  
   - `Apify (Skyscanner API)`, `Open-Meteo API`, `Rapid API (Booking.com API)`, `Google Places API` 호출  
   - **Airportal** 사이트에서 **인천공항 출/도착 현황** 데이터 크롤링  
   - 모든 원본 데이터는 **S3** (`team5-s3/raw_data`)에 적재  

2. **데이터 변환:**  
   - **AWS Glue**를 통해 데이터 변환 후 **Parquet** 형식으로 **S3**(`team5-s3/transform_data`)에 저장  

3. **데이터 적재:**  
   - 변환된 데이터는 **RDS (PostgreSQL)**와 **Snowflake**에 적재  
   - **RDS**는 웹 서비스와 연결, **Snowflake**는 데이터 분석 및 대시보드에 활용  

4. **데이터 분석:**  
   - **Snowflake**에서 `TEAM5.RAW_DATA` → `TEAM5.ANALYTICS`로 분석 데이터 생성  
   - 최신 데이터 자동 반영을 위해 **VIEW** 활용  

5. **서비스 제공:**  
   - **RDS** → **Django** 웹 서비스  
   - **Snowflake** → **Preset** 대시보드  

<img src="https://github.com/user-attachments/assets/46e9fbcd-d13a-40dc-97cc-f0977f5189e3" width="800"/>

---
