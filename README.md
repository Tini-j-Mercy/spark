# spark
from selenium import webdriver

import time
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.common.keys import Keys
from selenium.common.exceptions import NoSuchElementException
from selenium.webdriver.support.ui import Select
from selenium.webdriver import ActionChains
from webdriver_manager.chrome import ChromeDriverManager
webdriver.Chrome(ChromeDriverManager().install())

opt = Options()
opt.add_argument("start-maximized")
opt.add_argument("--disable-extensions")
opt.add_experimental_option("prefs", { \
"profile.default_content_setting_values.media_stream_mic": 1,
"profile.default_content_setting_values.media_stream_camera": 1,
"profile.default_content_setting_values.geolocation": 1,
"profile.default_content_setting_values.notifications": 1
})

wdriver = webdriver.Chrome(ChromeDriverManager().install())
wdriver.maximize_window()
wdriver.get("https://www.thesparksfoundationsingapore.org/")


# Test 1:check Title
print("\nTestCase 1:")
if wdriver.title:
    print("\nTitle Verified Successfully: ", wdriver.title)
else:
    print("\nTitle Verification Failed!\n")

# Test 2: check logo
print("\nTestCase 2:")
try:
    wdriver.find_element_by_xpath('//*[@id="home"]/div/div[1]/h1/a/*').click()
    print('Success! The logo is present\n')
    time.sleep(3)
except NoSuchElementException:
    print('No logo is present!\n')

# Test 3: Check for navbar 
print("TestCase 3:")
try:
    wdriver.find_element_by_class_name("navbar")
    print("Navbar Verification Successful!\n")
except NoSuchElementException:
    print("Navbar Verification Failed!\n")

# Test 4:check for Home button
print("TestCase 4:")
try:
    wdriver.find_element_by_partial_link_text("The Sparks Foundation").click()
    print("Home link is working!\n")
except NoSuchElementException:
    print("Home Link Doesn't Work!\n")


# Test 5:check for About Us Page
print("TestCase 5:")
try:
    wdriver.find_element_by_link_text('About Us').click()
    time.sleep(3)
    wdriver.find_element_by_link_text('Corporate Partners').click()
    time.sleep(3)
    print('Page visited Successfully!\n')
except NoSuchElementException:
    print("Page visit Failed! Does not exist.\n")
    time.sleep(3)

# Test 6:check for Policy page
print('TestCase 6:')
try:
    wdriver.find_element_by_link_text('Policies and Code').click()
    time.sleep(3)
    wdriver.find_element_by_link_text("Policies").click()
    time.sleep(3)
    wdriver.find_element_by_link_text('Code of Ethics and Conduct').click()
    time.sleep(3)
    print('Policy Page Verified!\n')
except NoSuchElementException:
    print('No New Tab opened. Failed!\n')

#test7 :check for programs
program = wdriver.find_element_by_xpath('//*[@id="link-effect-3"]/ul/li[3]/a')
mentor = wdriver.find_element_by_xpath('//*[@id="link-effect-3"]/ul/li[3]/ul/li[2]/a')

actions = ActionChains(wdriver)

actions.move_to_element(program).click().move_to_element(mentor).click().perform()
time.sleep(9)

wdriver.execute_script("window.scrollBy(0,600)", "")
time.sleep(10)


# Test 8: Check the Contact us Page
print("TestCase 8:")
try:
    wdriver.find_element_by_link_text("Contact Us").click()
    time.sleep(3)
    info = wdriver.find_element_by_xpath('/html/body/div[2]/div/div/div[3]/div[2]/p[2]')
    time.sleep(3)

    # print(info.text)
    if info.text == "+65-8402-8590, info@thesparksfoundation.sg":
        print('Contact Information is Correct!')
    else:
        print('Contact Information is Incorrect!')
    print("Contact Page Verification Sucessful!\n")
except NoSuchElementException:
    print("Contact Page Verification Unsuccessful!")

# Test 9: check for Links Page
print("TestCase 9:")
try:
    wdriver.find_element_by_link_text('LINKS').click()
    time.sleep(3)
    wdriver.find_element_by_link_text('Software & App').click()
    time.sleep(3)
    wdriver.find_element_by_link_text('AI in Education').click()
    time.sleep(3)
    print('LINKS Verfication Successful!\n')
except NoSuchElementException:
    print("LINKS Verification Failed!\n")

# Test 10: Check the Form
print("TestCase 10:")
try:
    wdriver.find_element_by_link_text('Join Us').click()
    time.sleep(3)
    wdriver.find_element_by_link_text('Why Join Us').click()
    time.sleep(3)
    wdriver.find_element_by_name('Name').send_keys('Tini J Mercy')
    time.sleep(3)
    wdriver.find_element_by_name('Email').send_keys('tinijmercy2001@gmail.com')
    time.sleep(3)
    select = Select(wdriver.find_element_by_class_name('form-control'))
    time.sleep(3)
    select.select_by_visible_text('Intern')
    time.sleep(3)
    wdriver.find_element_by_class_name('button-w3layouts').click()
    time.sleep(3)
    print("Form Verification Successful!\n")
except NoSuchElementException:
    print("Form Verification Failed!\n")
    time.sleep(3)


cls = wdriver.close()
