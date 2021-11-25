# selenium

## chromedrive 오류

> 개발자를 확인할 수 없기 때문에 ‘chromedriver’을(를) 열 수 없습니다.

```python
driver.get('chrome://settings/advanced')
driver.find_element_by_id('privacyContentSettingsButton').click()
driver.find_element_by_name('popups').click()
```

### 해결책

터미널 열고 chromedriver가 위치한 디렉토리에서 다음의 명령어 실행

```bash
xattr -d com.apple.quarantine chromedriver
```


## 엘리먼트 존재 확인

```python
from selenium.common.exceptions import NoSuchElementException

def check_exists_by_class(class_name):
    try:
        driver.find_element(By.CLASS_NAME, class_name)
    except NoSuchElementException:
        return False
    return True
```


## alert 표시 여부 확인
```python
from selenium.common.exceptions import NoAlertPresentException

def is_alert_present():
    try:
        driver.switch_to.alert()
        return True
    except NoAlertPresentException:
        return False

```