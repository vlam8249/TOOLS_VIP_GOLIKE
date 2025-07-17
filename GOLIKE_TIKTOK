import json
import os,time
import cloudscraper
import requests
import socket
import subprocess
from time import strftime
from time import sleep
from datetime import datetime, timedelta
from bs4 import BeautifulSoup
import time
from colorama import Fore, init
import sys

def kiem_tra_mang():
    try:
        socket.create_connection(("8.8.8.8", 53), timeout=3)
    except OSError:
        print("Mạng không ổn định hoặc bị mất kết nối. Vui lòng kiểm tra lại mạng.")

kiem_tra_mang()
scraper = cloudscraper.create_scraper()

from colorama import Fore

banner = f"""
{Fore.YELLOW}╔════════════════════════════════════════════════════════╗
{Fore.YELLOW}║                                                        ║
{Fore.YELLOW}║   \033[38;2;0;120;255m████████╗ ██████╗  ██████╗ ██╗     \033[0m{Fore.YELLOW}║
{Fore.YELLOW}║   \033[38;2;0;140;255m╚══██╔══╝██╔═══██╗██╔═══██╗██║     \033[0m{Fore.YELLOW}║
{Fore.YELLOW}║   \033[38;2;0;160;255m   ██║   ██║   ██║██║   ██║██║     \033[0m{Fore.YELLOW}║
{Fore.YELLOW}║   \033[38;2;0;180;255m   ██║   ██║   ██║██║   ██║██║     \033[0m{Fore.YELLOW}║
{Fore.YELLOW}║   \033[38;2;0;200;255m   ██║   ╚██████╔╝╚██████╔╝███████╗\033[0m{Fore.YELLOW}║
{Fore.YELLOW}║   \033[38;2;0;220;255m   ╚═╝    ╚═════╝  ╚═════╝ ╚══════╝\033[0m{Fore.YELLOW}║
{Fore.YELLOW}║                                                        ║
{Fore.YELLOW}╚════════════════════════════════════════════════════════╝
{Fore.WHITE}════════════════════════════════════════════════════════════
{Fore.RED}{Fore.WHITE}Phiên Bản: {Fore.YELLOW}TOOL_GOLIKE_TIKTOK_║ ADMIN: \033[38;2;0;220;255mVILÂM
{Fore.WHITE}════════════════════════════════════════════════════════════
[{Fore.RED}⚡{Fore.WHITE}] Zalo: \033[38;2;0;220;255m0368782618
[{Fore.RED}⚡{Fore.WHITE}] Lưu ý: \033[38;2;0;220;255mAE dùng tool bị lỗi thì gọi ADMIN để sửa
{Fore.WHITE}════════════════════════════════════════════════════════════
 TOOL này có lọc tài khoản riêng tư TIKTOK 
{Fore.WHITE}════════════════════════════════════════════════════════════
"""
os.system('cls' if os.name== 'nt' else 'clear')
print(banner)
print("\033[1;35m╔═════════════════════════════════╗")
print("\033[1;35m║       \033[1;33m  ĐĂNG NHẬP GOLIKE        \033[1;35m║")
print("\033[1;35m╚═════════════════════════════════╝") 
    # Nhập auth
try:
  Authorization = open("Authorization.txt","x")
  t = open("token.txt","x")
except:
  pass
Authorization = open("Authorization.txt","r")
t = open("token.txt","r")
author = Authorization.read()
token = t.read()
if author == "":
  author = input("\033[1;32mNHẬP AUTHORIZATION : \033[1;33m")
  token = input("\033[1;32mNHẬP T (Token) : \033[1;33m")
  Authorization = open("Authorization.txt","w")
  t = open("token.txt","w")
  Authorization.write(author)
  t.write(token)
else:
  print(f"\033[1;32m       Nhấn Enter để vào TOOL")
  print(f"\033[38;2;0;220;255m               HOẶC ")
  select = input(f"\033[1;32mNhập AUTHORIZATION {Fore.RED}(tại đây) \033[1;32mđể vào acc khác: \033[1;33m")
  kiem_tra_mang()
  if select != "":
    author = select
    token = input("\033[1;32mNhập T (Token) : \033[1;33m")
    Authorization = open("Authorization.txt","w")
    t = open("token.txt","w")
    Authorization.write(author)
    t.write(token)
Authorization.close()
t.close()
os.system('cls' if os.name== 'nt' else 'clear')
print(banner)
print("\033[1;35m╔═════════════════════════════════╗")
print("\033[1;35m║   \033[1;33m   DANH SÁCH ACC TIKTOK       \033[1;35m║")
print("\033[1;35m╚═════════════════════════════════╝")  
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
    response = scraper.get(
        'https://gateway.golike.net/api/tiktok-account',
        headers=headers,
        json=json_data
    ).json()
    return response
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
        return response.json()
    except Exception as e:
        print()
        return {}
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
            timeout=6
        )
        return response.json()
    except Exception as e:
        print()
        return {}
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
    except Exception as e:
        print()
# Gọi chọn tài khoản một lần và xử lý lỗi nếu có
chontktiktok = chonacc()
def dsacc():
  if chontktiktok.get("status") != 200:  
    print("\033[1;31mAuthorization hoăc T sai   ")
    quit()
  for i in range(len(chontktiktok["data"])):
    print(f'\033[1;36m[{i+1}]\033[1;93m {chontktiktok["data"][i]["nickname"]} \033[1;97m|\033[1;31m\033[1;32m Hoạt Động')
dsacc() 
print(f"{Fore.MAGENTA}═══════════════════════════════════")
while True:
  try:
    luachon = int(input("\033[1;32mChọn tài khoản TIKTOK: \033[1;33m"))
    while luachon > len((chontktiktok)["data"]):
      luachon = int(input("\033[1;32mAcc Này Không Có Trong Danh Sách , Nhập Lại : \033[1;33m"))
    account_id = chontktiktok["data"][luachon - 1]["id"]
    break  
  except:
    print("\033[1;31mSai Định Dạng   ") 
while True:
  try:
    delay = int(input(f"\033[1;32mDelay: \033[1;33m"))
    break
  except:
    print("\033[1;31mSai Định Dạng  ")
while True:
  try: 
    doiacc = int(input(f"\033[1;32mThất bại bao nhiêu lần thì đổi acc: \033[1;33m"))
    break
  except:
    print("\033[1;31mNhập Vào 1 Số  ")  
print("\033[1;35m╔═════════════════════════════════╗")
print("\033[1;35m║     \033[1;33m  CHỌN LOẠI NHIỆM VỤ        \033[1;35m║")
print("\033[1;35m╚═════════════════════════════════╝")
print("\033[1;36m[1] \033[1;32mFollow")
print("\033[1;36m[2] \033[1;32mLike")
print("\033[1;36m[3] \033[1;32mCả hai (\033[1;33mFollow và Like\033[1;32m)")
while True:
    try:
        loai_nhiem_vu = int(input("\033[1;32mChọn loại nhiệm vụ: \033[1;33m"))
        if loai_nhiem_vu in [1, 2, 3]:
            break
        else:
            print("\033[1;31mVui lòng chọn số từ 1 đến 3!")
    except:
        print("\033[1;31mSai định dạng! Vui lòng nhập số.")  
x_like, y_like, x_follow, y_follow = None, None, None, None
print("\033[1;35m╔═════════════════════════════════╗")
print("\033[1;35m║       \033[1;33m  ADB tự động             \033[1;35m║")
print("\033[1;35m╚═════════════════════════════════╝")
print(f"\033[1;36m[1] Có")
print(f"\033[1;36m[2] Không")
adbyn = input(f"\033[1;32mNhập lựa chọn: \033[1;33m")
if adbyn == "1":
    def setup_adb():
      config_file = "adb_config.txt"
      like_coords_file = "toa_do_tim.txt"
      follow_coords_file = "toa_do_follow.txt"
    # Nhập IP và port ADB
      print(f"{Fore.MAGENTA}═══════════════════════════════════")
      
      ip = input("\033[1;32mNhập IP của thiết bị ví dụ (192.168.1.2): \033[1;33m")
      adb_port = input("\033[1;32mNhập port của thiết bị ví dụ (39327): \033[1;33m")
      # Kiểm tra và đọc tọa độ từ file nếu tồn tại
      x_like, y_like, x_follow, y_follow = None, None, None, None    
      if os.path.exists(like_coords_file):
           with open(like_coords_file, "r") as f:
              coords = f.read().split("|")
              if len(coords) == 2:
                   x_like, y_like = coords
                   print(f"\033[1;32mĐã tìm thấy tọa độ nút tim: X={x_like}, Y={y_like}")    
      if os.path.exists(follow_coords_file):
          with open(follow_coords_file, "r") as f:
               coords = f.read().split("|")
               if len(coords) == 2:
                   x_follow, y_follow = coords
                   print(f"\033[1;32mĐã tìm thấy tọa độ nút follow: X={x_follow}, Y={y_follow}")
      if not os.path.exists(config_file):
           print("\033[1;36mLần đầu chạy, nhập mã ghép nối (6 SỐ) và port ghép nối.\033[0m")
           pair_code = input("\033[1;32mNhập mã ghép nối 6 số ví dụ (322763): \033[1;33m")
           pair_port = input("\033[1;32mNhập port ghép nối ví dụ (44832): \033[1;33m")
           with open(config_file, "w") as f:
               f.write(f"{pair_code}|{pair_port}")
      else:
          with open(config_file, "r") as f:
               pair_code, pair_port = [s.strip() for s in f.read().split("|")]  
      print("\n\033[1;36m  Đang ghép nối với thiết bị\033[0m")
      os.system(f"adb pair {ip}:{pair_port} {pair_code}")
      time.sleep(2)  
      print("\033[1;36m  Đang kết nối ADB\033[0m")
      os.system(f"adb connect {ip}:{adb_port}")
      time.sleep(2)  
      devices = os.popen("adb devices").read()
      if ip not in devices:
        print(f"{Fore.RED} Kết nối thất bại{Fore.WHITE}")
        exit()    
       # Yêu cầu nhập tọa độ nếu chưa có
      print("\033[1;35m╔═════════════════════════════════╗")
      print("\033[1;35m║     \033[1;33m  NHẬP TỌA ĐỘ NÚT         \033[1;35m║")
      print("\033[1;35m╚═════════════════════════════════╝")    
      if loai_nhiem_vu in [1, 3] and (x_follow is None or y_follow is None):
           x_follow = input("\033[1;32mNhập tọa độ X của nút follow: \033[1;33m")
           y_follow = input("\033[1;32mNhập tọa độ Y của nút follow: \033[1;33m")
           with open(follow_coords_file, "w") as f:
               f.write(f"{x_follow}|{y_follow}")    
      if loai_nhiem_vu in [2, 3] and (x_like is None or y_like is None):
           x_like = input("\033[1;32mNhập tọa độ X của nút tim: \033[1;33m")
           y_like = input("\033[1;32mNhập tọa độ Y của nút tim: \033[1;33m")
           with open(like_coords_file, "w") as f:
              f.write(f"{x_like}|{y_like}")
      return x_like, y_like, x_follow, y_follow
# Khi gọi hàm setup_adb()
    x_like, y_like, x_follow, y_follow = setup_adb()
elif adbyn == "2":
    pass
# Thêm phần chọn loại nhiệm vụ sau khi chọn tài khoản và trước khi bắt đầu làm nhiệm vụ   
dem = 0
tong = 0
checkdoiacc = 0
dsaccloi = []
accloi = ""
os.system('cls' if os.name== 'nt' else 'clear')
print(banner)
print("\033[1;37m════════════════════════════════════════════════════════════")
print("\033[1;31m| \033[1;36mSTT \033[1;37m| \033[1;33mThời gian \033[1;37m| \033[1;32mStatus \033[1;37m| \033[1;31mType job \033[1;37m| \033[1;32mID Acc \033[1;37m| \033[1;32mXu \033[1;37m| \033[1;33mTổng       ")
print("\033[1;37m════════════════════════════════════════════════════════════")
while True:
    if checkdoiacc == doiacc:
        dsaccloi.append(chontktiktok["data"][luachon - 1]["nickname"])
        print(f"{Fore.WHITE}════════════════════════════════════════════════════")
        print(f"\033[1;31m  Acc Tiktok {dsaccloi} gặp vấn đề ")
        print(f"{Fore.WHITE}════════════════════════════════════════════════════")
        dsacc()
        while True:
            try:
                print(f"{Fore.WHITE}════════════════════════════════════════════════════")
                luachon = int(input("\033[1;32mChọn tài khoản mới: \033[1;33m"))
                while luachon > len((chontktiktok)["data"]):
                    luachon = int(input("\033[1;31mAcc Này Không Có Trong Danh Sách, Hãy Nhập Lại : \033[1;33m"))
                account_id = chontktiktok["data"][luachon - 1]["id"]
                checkdoiacc = 0
                os.system('cls' if os.name== 'nt' else 'clear')
                for h in banner:
                    print(h,end = "")
                break  
            except:
                print("\033[1;31mSai Định Dạng !!!")
    print('\033[1;35mĐang Tìm Nhiệm Vụ', end="\r")
    max_retries = 3
    retry_count = 0
    nhanjob = None
    while retry_count < max_retries:
        try:
            nhanjob = nhannv(account_id)
            if nhanjob and nhanjob.get("status") == 200 and nhanjob["data"].get("link") and nhanjob["data"].get("object_id"):
                break
            else:
                retry_count += 1
                time.sleep(2)
        except Exception as e:
            retry_count += 1
            time.sleep(1)
    if not nhanjob or retry_count >= max_retries:
        continue
    ads_id = nhanjob["data"]["id"]
    link = nhanjob["data"]["link"]
    object_id = nhanjob["data"]["object_id"]
    job_type = nhanjob["data"]["type"]
    # Kiểm tra loại nhiệm vụ
    if (loai_nhiem_vu == 1 and job_type != "follow") or \
       (loai_nhiem_vu == 2 and job_type != "like") or \
       (job_type not in ["follow", "like"]):
        baoloi(ads_id, object_id, account_id, job_type)
        continue
    # Mở link và kiểm tra lỗi
    try:
        if adbyn == "1":
            os.system(f'adb shell am start -a android.intent.action.VIEW -d "{link}" > /dev/null 2>&1')
        else:
            #os.system(f"termux-open-url {link}")
            subprocess.run(["termux-open-url", link])        
        for remaining in range(3, 0, -1):
            time.sleep(1)
        print("\r" + " " * 30 + "\r", end="")
    except Exception as e:
        baoloi(ads_id, object_id, account_id, job_type)
        continue
    # Thực hiện thao tác ADB
    if job_type == "like" and adbyn == "1" and x_like and y_like:
        os.system(f"adb shell input tap {x_like} {y_like}")
    elif job_type == "follow" and adbyn == "1" and x_follow and y_follow:
        os.system(f"adb shell input tap {x_follow} {y_follow}")
    # Đếm ngược delay
    for remaining_time in range(delay, -1, -1):
        color = "\033[1;36m" if remaining_time % 2 == 0 else "\033[1;33m"
        print(f"\r{color}| TOOL-VIP | {remaining_time}s           ", end="")
        time.sleep(1)    
    print("\r                          \r", end="") 
    print("\033[1;35mĐang Nhận Tiền    ",end = "\r")
    # Hoàn thành job
    max_attempts = 2
    attempts = 0
    nhantien = None
    while attempts < max_attempts:
        try:
            nhantien = hoanthanh(ads_id, account_id)
            if nhantien and nhantien.get("status") == 200:
                break
        except:
            pass  
        attempts += 1

    if nhantien and nhantien.get("status") == 200:
        dem += 1
        tien = nhantien["data"]["prices"]
        tong += tien
        local_time = time.localtime()
        hour = local_time.tm_hour
        minute = local_time.tm_min
        second = local_time.tm_sec
        h = hour
        m = minute
        s = second
        if hour < 10:
            h = "0" + str(hour)
        if minute < 10:
            m = "0" + str(minute)
        if second < 10:
            s = "0" + str(second)
                                      
        job_label = f"JOB {job_type.upper()}"
        chuoi = (f"[1;35m[[1;31m{dem}[1;35m]"
                 f" [1;35m[[1;32m{job_label}[1;35m]"
                 f" [1;35m[[38;2;0;180;255m{job_type}[1;35m]"
                 f" [1;35m[[1;33m+{tien}[1;35m]"
                 f" [1;35m[[1;33mTổng: {tong}[1;35m]"
                 f" [1;35m[[1;37mTime: {h}:{m}:{s}[1;35m]")

        print("                                                    ", end="\r")
        print(chuoi)
        time.sleep(0.7)
        checkdoiacc = 0
    else:
        try:
            baoloi(ads_id, object_id, account_id, nhanjob["data"]["type"])
            print("                                              ", end="\r")
            print("\033[1;31m🚀 Bỏ qua nhiệm vụ ", end="\r")
            sleep(1)
            checkdoiacc += 1
        except:
            pass
