# Windows 서비스 및 예약된 작업 비활성화

## 1. 개요
이 문서는 Windows의 특정 서비스 및 예약된 작업을 비활성화함으로써 얻을 수 있는 효과에 대해 설명합니다.<br>
이러한 작업을 수행하면 시스템 성능을 최적화하고 불필요한 백그라운드 작업을 줄일 수 있습니다.<br>
다만, 일부 기능 제한 및 보안 취약점 발생 가능성을 고려해야 합니다.

---

## 2. 비활성화되는 Windows 서비스와 효과

| 서비스 | 역할 | 비활성화 효과 |
|---------|---------------------------------|-------------------------------------------------------------|
| **BITS (Background Intelligent Transfer Service)** | 백그라운드에서 파일을 다운로드 및 업로드하는 서비스 (Windows 업데이트 및 기타 Microsoft 서비스에서 사용) | Windows 업데이트, Microsoft Store 다운로드 등이 느려지거나 실패할 가능성이 있음. 하지만 불필요한 백그라운드 데이터 사용을 차단하여 네트워크 대역폭을 절약할 수 있음. |
| **DiagTrack (Diagnostics Tracking Service, aka Connected User Experiences and Telemetry)** | Microsoft에 원격으로 진단 및 사용 데이터를 전송하는 서비스 | Windows의 원격 진단 데이터 수집을 막아 개인정보 보호 강화. 일부 Windows 기능(예: 피드백 허브, 추천 기능)이 제한될 수 있음. |
| **PcaSvc (Program Compatibility Assistant Service)** | 이전 Windows 버전용 프로그램의 호환성을 자동으로 조정하는 서비스 | 일부 구형 프로그램 실행 시 문제가 발생할 가능성이 있음. 하지만 불필요한 백그라운드 프로세스를 줄일 수 있음. |
| **SysMain (Superfetch, 기존 Prefetch)** | 자주 사용하는 프로그램을 미리 로드하여 성능을 높이는 기능 | SSD 환경에서는 성능 개선 효과가 크지 않으므로 불필요한 디스크 및 메모리 사용을 줄일 수 있음. |
| **WSearch (Windows Search, aka 인덱싱 서비스)** | 파일 검색 속도를 높이기 위해 색인을 생성하는 기능 | Windows 탐색기의 검색 기능이 느려질 수 있지만, 불필요한 디스크 및 CPU 사용량이 줄어들어 시스템 성능이 향상될 수 있음. |
| **wuauserv (Windows Update Service)** | Windows 업데이트를 담당하는 서비스 | 자동 업데이트가 비활성화되어 원치 않는 업데이트가 설치되지 않음. 하지만 보안 패치가 적용되지 않아 보안 취약점이 남을 수 있음. |

---

## 3. 비활성화되는 예약된 작업과 효과

| 예약 작업 | 역할 | 비활성화 효과 |
|--------------------------|-----------------------------------|-----------------------------------------------------------|
| **\Microsoft\Windows\Chkdsk\ProactiveScan** | 디스크 오류를 주기적으로 검사하는 예약 작업 | 자동 디스크 검사 기능이 비활성화됨. 디스크 상태를 수동으로 확인해야 하지만, 백그라운드 작업을 줄일 수 있음. |
| **\Microsoft\Windows\Windows Defender\Windows Defender Cache Maintenance** | Windows Defender의 캐시 유지보수 작업 | Defender 관련 프로세스의 리소스 사용 감소. 하지만 Windows Defender의 검사 속도가 느려질 수도 있음. |
| **\Microsoft\Windows\Windows Defender\Windows Defender Cleanup** | Windows Defender가 오래된 검사 결과를 정리하는 작업 | 오래된 검사 기록이 자동으로 정리되지 않으므로 수동 정리가 필요할 수 있음. |
| **\Microsoft\Windows\Windows Defender\Windows Defender Scheduled Scan** | 예약된 Windows Defender 정기 검사 | 실시간 보호 기능은 유지되지만, 예약 검사가 실행되지 않음. |
| **\Microsoft\Windows\Windows Defender\Windows Defender Verification** | Windows Defender의 기능을 확인하고 유지 관리하는 작업 | Windows Defender의 자동 유지 관리 기능이 비활성화됨. |
| **\Microsoft\Windows\WindowsUpdate\Scheduled Start** | 예약된 Windows 업데이트 시작 작업 | Windows가 자동으로 업데이트를 다운로드하거나 설치하지 않음. 보안 업데이트를 수동으로 확인해야 함. |

---

## 4. 장점과 단점

### ✅ 장점
- **시스템 리소스 사용 감소** → CPU, 메모리, 디스크 사용량 절약
- **불필요한 백그라운드 작업 차단** → 시스템 성능 최적화
- **자동 Windows 업데이트 차단** → 원치 않는 업데이트 설치 방지
- **개인정보 보호 강화** → 원격 데이터 전송 및 원격 진단 기능 비활성화

### ❌ 단점
- **Windows 업데이트 차단으로 보안 취약점 발생 가능** → 수동 업데이트 필요
- **Windows Defender 일부 기능 비활성화로 보안 취약 가능성** → 추가 보안 소프트웨어 필요
- **Windows 검색 및 프로그램 호환성 기능 일부 제한될 수 있음**
- **자동 유지보수 기능 비활성화로 디스크 및 시스템 상태를 수동으로 점검해야 함**

---

## 5. 추천 설정
✅ **Windows Update(wuauserv)는 주기적으로 실행하여 보안 업데이트 설치**<br>
✅ **Windows Defender 관련 작업은 유지하여 보안 취약점 방지**<br>
✅ **Windows 검색(WSearch)은 필요할 때만 비활성화하여 검색 기능 유지**<br>
✅ **Superfetch(SysMain)은 SSD 사용 환경에서만 비활성화**

이 설정을 통해 최적의 성능과 보안을 유지할 수 있습니다. 🚀

