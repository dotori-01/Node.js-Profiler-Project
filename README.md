# Node.js-Profiler-Project
Profiler를 독자적으로 개발

## 0. 프로그램 개요
 핵심 기능
멀티레이어 아키텍처: 프레젠테이션/비즈니스/데이터 계층 분리
고성능 데이터 처리: 스트림 기반 대용량 파일 처리(10GB+ 지원)
확장 가능 통계 엔진: MIN/MAX/AVG + 표준편차/백분위수 계산
실시간 시각화: WebSocket + Chart.js 기반 대화형 차트
DB 통합: MySQL + Redis 캐싱 계층
보안 강화: JWT 인증 + 역할 기반 접근 제어

기술 스택  

## 1. 프로그램 수행 절차 분석
     [웹 클라이언트] ←HTTP/WebSocket→ [Nginx]
                          ↓
                  [Node.js API 서버]
                    ↙       ↘
               [MySQL]     [Redis]
# 데이터 처리 파이프라인
1. 파일 업로드
Multer 미들웨어를 통한 안전한 파일 수신
확장자(.txt) 및 MIME 타입(text/plain) 검증
SHA-256 해시 기반 파일명 암호화

2. 데이터 파싱
       const readInterface = readline.createInterface({
        input: fs.createReadStream(filePath),
        crlfDelay: Infinity
      });
 
      readInterface.on('line', processLine);
3. 통계 계산
기본 메트릭: Math.min(), Math.max(), Array.reduce()
확장 메트릭: Welford 알고리즘 기반 표준편차

4. 데이터 저장
MySQL: 정규화된 테이블 구조
Redis: 실시간 캐싱(5분 TTL)

5. 시각화 처리
WebSocket을 통한 실시간 데이터 전송
Chart.js 커스텀 플러그인 구현

