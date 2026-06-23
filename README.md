### 서포트사이트 플러그인 (imkun85 패치)

[flaskfarm/support_site](https://github.com/flaskfarm/support_site)를 포크해서 버그 하나를 고친 버전이다.

수정한 파일은 `site_watcha.py` 하나다.

`get_json()` 메서드에서 `SiteUtil.get_response()` 호출 시 `timeout` 인자가 없었다.
왓챠(Watcha) API 서버가 응답을 안 하면 gevent 워커가 무한 대기 상태에 빠지고,
결국 FlaskFarm2 전체가 hang되어 NAS 재부팅이 필요했다.

`timeout=30`을 추가해서 최대 30초 후 타임아웃으로 hang을 방지했다.