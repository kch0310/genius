import csv, folium

count_csv = 0
base_map = folium.Map(location = [37.5642135, 127.0016985],zoom_start = 12)


#-----데이터 처리-----
find_file = input('파일 경로 or 이름을 입력하세요(파일명.csv) : ')
#route_file = "'.//"+find_file+"'"
#print(route_file)
csvfile = open(find_file, 'r', encoding='utf-8')
readcsv = csv.reader(csvfile)
for csv_inf in readcsv:
    if count_csv == 0:
        print('프로그램 실행 중...')
        count_csv += 1
    else:
        count_csv += 1
        latitude = float(csv_inf[9])
        longitude = float(csv_inf[10])
        area = csv_inf[1]
        folium.Marker([latitude, longitude], popup=area).add_to(base_map)
        #print(csv_inf)
        
csvfile.close()
base_map.save('./공사현황지도.html')
print('실행완료')
    
    
#-----지도&웹사이트 만들기-----
base_map_read = open('./공사현황지도.html', 'r')
make_website = open("website.html", 'w')

html_text = '''
<!DOCTYPE html>
<html>
<head>
   <meta charset="UTF-8">
   <style>
        header{border-bottom:1px solid gray;padding:20px;}
        nav{border-right:1px solid gray; width:250px; height:600px; float:left;}
        article{width:700px;height:600px;float:left;}
    </style>
</head>
<body>

</body>
</html>
'''


#지도 html코드 가져와서 붙여넣기
lines = base_map_read.readlines()
for line in lines:
    print(line)

make_website.write(html_text)
base_map_read.close()
make_website.close()
