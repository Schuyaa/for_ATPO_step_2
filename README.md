# for_ATPO_step_2

Тестирование Тестова Тестовича

from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import math

# функция для вычисления значения
def calc(x):
    return str(math.log(abs(12 * math.sin(int(x)))))

# открываем браузер
browser = webdriver.Chrome()

try:
    browser.get("http://suninjuly.github.io/explicit_wait2.html")

    # ждем, пока цена не станет $100
    WebDriverWait(browser, 15).until(
        EC.text_to_be_present_in_element((By.ID, "price"), "$100")
    )

    # нажимаем на кнопку "Book"
    browser.find_element(By.TAG_NAME, "button").click()

    # находим значение x и решаем задачу
    x_element = browser.find_element(By.ID, "input_value")
    x = x_element.text
    answer = calc(x)

    # вводим ответ в поле
    browser.find_element(By.ID, "answer").send_keys(answer)

    # отправляем форму
    browser.find_element(By.ID, "solve").click()

finally:
    # не закрываем браузер сразу, чтобы увидеть число
    WebDriverWait(browser, 10).until(EC.alert_is_present())
    alert = browser.switch_to.alert
    print(alert.text)  # ответ будет содержаться в тексте алерта
    alert.accept()