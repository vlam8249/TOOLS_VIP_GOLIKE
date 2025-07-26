import json
import os
import time
import cloudscraper
import requests
import webbrowser
from bs4 import BeautifulSoup
from colorama import Fore, init
from rich.table import Table
from rich.console import Console
from rich.panel import Panel
from rich import box
import sys
init() 
os.system('clear')
init(autoreset=True)
console = Console()
# Nhập auth
try:
    with open("Auth.txt", "x"):
        pass
    with open("token.txt", "x"):
        pass
except:
    pass

try:
    with open("Auth.txt", "r") as Auth, open("token.txt", "r") as t:
        author = Auth.read().strip()
        token = t.read().strip()
except:
    print("\033[1;31m Hãy tạo file Auth.txt và token.txt!\n")
    sys.exit(1)

os.system('clear')

print(f"[1] Sử dụng Authorization và Token hiện tại")
print(f"[2] Nhập Authorization và Token mới")
select = input(f"Nhập lựa chọn (1 hoặc 2): \033[1;33m").strip()

if select == "1":
    if not author or not token:
        print("\033[1;31mCredential files are empty!\n")
        sys.exit(1)
    print(f"\033[1;32mSử dụng Authorization và Token hiện tại\n")
elif select == "2":
    author = input("NHẬP AUTHORIZATION GOLIKE: ").strip()
    token = input("NHẬP TOKEN (T CỦA GOLIKE): ").strip()
    try:
        with open("Auth.txt", "w") as Auth, open("token.txt", "w") as t:
            Auth.write(author)
            t.write(token)
    except:
        print("\033[1;31m Hãy tạo file Auth.txt và token.txt!\n")
        sys.exit(1)
else:
    print("\033[1;31mLựa chọn không hợp lệ! Vui lòng chọn 1 hoặc 2.")
    sys.exit(1)

os.system('clear')
print("                     DANH SÁCH ACC TIKTOK               ")
print(f"{Fore.MAGENTA}===================================")

headers = {
    'Accept': 'application/json, text/plain, */*',
    'Content-Type': 'application/json;charset=utf-8',
    'Authorization': author,
    't': token,
    'User-Agent': 'Mozilla/5.0 (Linux; Android 10; K) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Mobile Safari/537.36',
    'Referer': 'https://app.golike.net/account/manager/tiktok',
}

scraper = cloudscraper.create_scraper()

def chonacc():
    json_data = {}
    try:
        response = scraper.get(
            'https://gateway.golike.net/api/tiktok-account',
            headers=headers,
            json=json_data
        )
        response.raise_for_status()
        data = response.json()
        if not isinstance(data, dict) or 'status' not in data:
            print(f"\033[1;31mInvalid account response: {data}")
            sys.exit(1)
        return data
    except requests.exceptions.RequestException as e:
        print(f"\033[1;31mError fetching accounts: {e}")
        sys.exit(1)

def nhannv(account_id):
    try:
        params = {
            'account_id': account_id,
            'data': 'null',
        }
        response = scraper.get(
            'https://gateway.golike.net/api/advertising/publishers/tiktok/jobs',
            headers=headers,
            params=params,
            json={}
        )
        response.raise_for_status()
        data = response.json()
        if not isinstance(data, dict) or 'status' not in data:
            print(f"\033[1;31mInvalid job response: {data}\n")
            return None
        return data
    except requests.exceptions.RequestException as e:
        return None

def hoanthanh(ads_id, account_id):
    try:
        json_data = {
            'ads_id': ads_id,
            'account_id': account_id,
            'async': True,
            'data': None,
        }
        response = scraper.post(
            'https://gateway.golike.net/api/advertising/publishers/tiktok/complete-jobs',
            headers=headers,
            json=json_data,
            timeout=20
        )
        response.raise_for_status()
        data = response.json()
        if not isinstance(data, dict) or 'status' not in data:
            print(f"\033[1;31mInvalid complete job response: {data}")
            return None
        if data.get("status") != 200 and "already" in data.get("message", "").lower():
            return {"status": "already_completed", "message": data.get("message", "")}
        return data
    except requests.exceptions.HTTPError as e:
        return None
    except requests.exceptions.RequestException as e:
        return None
    except ValueError as e:
        return None

def baoloi(ads_id, object_id, account_id, loai):
    try:
        json_data1 = {
            'description': 'Tôi đã làm Job này rồi',
            'users_advertising_id': ads_id,
            'type': 'ads',
            'provider': 'tiktok',
            'fb_id': account_id,
            'error_type': 6,
        }
        scraper.post('https://gateway.golike.net/api/report/send', headers=headers, json=json_data1)
        json_data2 = {
            'ads_id': ads_id,
            'object_id': object_id,
            'account_id': account_id,
            'type': loai,
        }
        scraper.post(
            'https://gateway.golike.net/api/advertising/publishers/tiktok/skip-jobs',
            headers=headers,
            json=json_data2,
        )
    except Exception:
        pass

def open_tiktok_link(link):
    try:
        os.system(f"termux-open-url '{link}'")
        time.sleep(2)
    except Exception:
        try:
            webbrowser.open(link)
            time.sleep(2)
        except Exception as e:
            print(f"\033[1;31mKhông mở được link tự động: {e}")
            print(f"\033[1;33mVui lòng mở link : {link}")

def countdown_delay(seconds, nickname, price_str, job_count, total, link, status):
    for i in range(seconds, -1, -1):
        display_dashboard(nickname, price_str, job_count, total, link, status, f"{i}...")
        time.sleep(1)
    display_dashboard(nickname, price_str, job_count, total, link, status, "")

def display_dashboard(nickname, price_str, job_count, total, link, status, delay_str):
    os.system('clear')  # Clear terminal

    table = Table(title="📋 THÔNG TIN JOB GOLIKE", box=box.ROUNDED, border_style="bold white")
    table.add_column("📌 Mục", justify="right", style="bold cyan")
    table.add_column("📤 Thông tin", justify="left", style="bold magenta")

    table.add_row("👤 Nick TikTok", nickname)
    table.add_row("💰 Giá", price_str)
    table.add_row("✅ Job thành công", str(job_count))
    table.add_row("💵 Tổng xu", str(total))
    table.add_row("🔗 Link job", link)
    table.add_row("📡 Trạng thái", status)
    table.add_row("⏳ Delay", delay_str)

    console.print(table)
    console.print(Panel.fit("🌟 [bold green]Chúc bạn bào GoLike vắt cực khô 😆[bold green]", border_style="green"))


chontktiktok = chonacc()

def dsacc():
    if chontktiktok.get("status") != 200:
        print("\033[1;31m Authorization hoặc T sai\n")
        sys.exit(1)
    for i in range(len(chontktiktok["data"])):
        print(f"\033[1;36m[{i+1}]\033[1;93m {chontktiktok['data'][i]['nickname']}")

dsacc()
print(f"{Fore.MAGENTA}===================================")

while True:
    try:
        luachon = int(input("\033[1;31mChọn tài khoản TIKTOK bạn muốn chạy : \033[1;33m"))
        if 1 <= luachon <= len(chontktiktok["data"]):
            account_id = chontktiktok["data"][luachon - 1]["id"]
            account_nickname = chontktiktok["data"][luachon - 1]["nickname"]
            break
        print("\033[1;31mAcc không có trong danh sách. Nhập lại!")
    except:
        print("\033[1;31mSai Định Dạng")

while True:
    try:
        delay = int(input(f"\033[1;32mDelay thực hiện job : \033[1;33m"))
        if delay >= 0:
            break
        print("\033[1;31mDelay phải là số không âm!")
    except:
        print("\033[1;31mSai Định Dạng")

while True:
    try:
        doiacc = int(input(f"\033[1;32mThất bại bao nhiêu lần thì đổi acc tiktok : \033[1;33m"))
        if doiacc > 0:
            break
        print("\033[1;31mSố lần thất bại phải lớn hơn 0!")
    except:
        print("\033[1;31m Nhập Sai \n")

dem = 0
tong = 0
checkdoiacc = 0
current_link = "N/A"
price_display = "Chưa check"
current_status = "Khởi động"

os.system('clear')

while True:
    if checkdoiacc >= doiacc:
        current_status = "Đổi acc TikTok"
        display_dashboard(account_nickname, price_display, dem, tong, current_link, current_status, "")
        print(f" {account_nickname} gặp vấn đề ({checkdoiacc} lần thất bại) ")
        dsacc()
        while True:
            try:
                print(f"{Fore.WHITE}====================================")
                luachon = int(input("\033[1;32m Chọn tài khoản mới đê : \033[1;33m"))
                if 1 <= luachon <= len(chontktiktok["data"]):
                    account_id = chontktiktok["data"][luachon - 1]["id"]
                    account_nickname = chontktiktok["data"][luachon - 1]["nickname"]
                    checkdoiacc = 0
                    current_status = "Khởi động"
                    display_dashboard(account_nickname, price_display, dem, tong, current_link, current_status, "")
                    break
                print("\033[1;31mAcc không hợp lệ. Nhập lại!\n")
            except:
                print("\033[1;31mSai định dạng\n")

    max_retries = 3
    retry_count = 0
    nhanjob = None
    current_status = "Lấy job"
    display_dashboard(account_nickname, price_display, dem, tong, current_link, current_status, "")

    while retry_count < max_retries:
        nhanjob = nhannv(account_id)
        if nhanjob and nhanjob.get("status") == 200 and nhanjob["data"].get("link") and nhanjob["data"].get("object_id"):
            break
        retry_count += 1
        time.sleep(2)

    if not nhanjob or retry_count >= max_retries:
        current_status = "Không lấy được job"
        display_dashboard(account_nickname, price_display, dem, tong, current_link, current_status, "")
        time.sleep(1)
        checkdoiacc += 1
        continue

    ads_id = nhanjob["data"]["id"]
    current_link = nhanjob["data"]["link"]
    object_id = nhanjob["data"]["object_id"]
    job_type = nhanjob["data"]["type"]

    time.sleep(3)  
# 3 giây check giá
    if "price_per_after_cost" not in nhanjob["data"]:
        price_display = "Không có giá"
        current_status = "Bỏ qua job"
        display_dashboard(account_nickname, price_display, dem, tong, current_link, current_status, "")
        baoloi(ads_id, object_id, account_id, job_type)
        time.sleep(1)
        current_link = "N/A"
        continue

    job_price = nhanjob["data"]["price_per_after_cost"]
    price_color = "\033[1;32m" if job_price == 42 else "\033[1;31m"
    price_symbol = "=" if job_price == 42 else "≠"
    price_display = f"{job_price} {price_color}{price_symbol}\033[0m 42"
    display_dashboard(account_nickname, price_display, dem, tong, current_link, current_status, "")
#
    if job_price != 42:
        current_status = "Bỏ qua job"
        display_dashboard(account_nickname, price_display, dem, tong, current_link, current_status, "")
        baoloi(ads_id, object_id, account_id, job_type)
        time.sleep(1)
        current_link = "N/A"
        price_display = "Chưa check"
        continue

    if job_type != "follow":
        current_status = "Bỏ qua job"
        display_dashboard(account_nickname, price_display, dem, tong, current_link, current_status, "")
        baoloi(ads_id, object_id, account_id, job_type)
        time.sleep(1)
        current_link = "N/A"
        price_display = "Chưa check"
        continue

    current_status = "Làm job"
    display_dashboard(account_nickname, price_display, dem, tong, current_link, current_status, "")
    open_tiktok_link(current_link)
    countdown_delay(delay, account_nickname, price_display, dem, tong, current_link, current_status)

    current_status = "Nhận tiền"
    display_dashboard(account_nickname, price_display, dem, tong, current_link, current_status, "")
    time.sleep(0.5)
#nhận 5 lần ko dc bỏ job
    max_attempts = 5
    attempts = 0
    nhantien = None
    while attempts < max_attempts:
        nhantien = hoanthanh(ads_id, account_id)
        if nhantien and (nhantien.get("status") == 200 or nhantien.get("status") == "already_completed"):
            break
        attempts += 1
        time.sleep(1)

    if nhantien and nhantien.get("status") == 200:
        dem += 1
        tien = nhantien["data"].get("price_per_after_cost", job_price)
        if tien == 0:
            print(f"\033[1;31m Lỗi nhận tiền\n")
        tong += tien
        current_status = "Thành Công"
        display_dashboard(account_nickname, price_display, dem, tong, current_link, current_status, "")
        time.sleep(0.7)
        checkdoiacc = 0
    elif nhantien and nhantien.get("status") == "already_completed":
        current_status = "Bỏ qua job vì đã nhận"
        display_dashboard(account_nickname, price_display, dem, tong, current_link, current_status, "")
        baoloi(ads_id, object_id, account_id, job_type)
        time.sleep(1)
    else:
        current_status = "Nhận tiền lỗi"
        display_dashboard(account_nickname, price_display, dem, tong, current_link, current_status, "")
        baoloi(ads_id, object_id, account_id, job_type)
        time.sleep(1)
        checkdoiacc += 1

    current_link = "N/A"
    price_display = "Chưa check"
