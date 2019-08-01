import urllib.parse,urllib.request
import json
import csv,codecs

url = 'https://api.shuidichou.com/api/cf/v5/detail/get'
headers = {"User-Agent":"Mozilla/5.0 (Windows NT 6.3; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.92 Safari/537.36"}

httpproxy_handler = urllib.request.ProxyHandler({"http":"123.139.56.238:9999"})
opener = urllib.request.build_opener(httpproxy_handler)
urllib.request.install_opener(opener)

# def write_txt(text):
#     with open(r'C:\Users\Administrator\Desktop\shuidichou.txt', 'a', encoding='utf-8') as f:
#         lists = text['data']['list']
#         for alist in lists:
#             nickname = str(alist['nickname'])
#             amt = str(alist['amt'])
#             image = str(alist['headImgUrl'])
#             f.write(nickname)
#             f.write(' ')
#             f.write(amt)
#             f.write(' ')
#             f.write(image)
#             f.write('\n')

def write_txt(text):
    with codecs.open(r'C:\Users\Administrator\Desktop\shuidichou.csv', 'a', 'utf_8_sig') as c:
        writer = csv.writer(c)
        lists = text['data']['list']
        for alist in lists:
            nickname = str(alist['nickname'])
            amt = str(alist['amt'])
            image = str(alist['headImgUrl'])
            writer.writerow([nickname,amt,image])

def main():
    hasNext = True
    anchorId = ''
    pageNum = 1

    while hasNext:
        formdata = {
            "size":"20",
            "infoUuid":"",
            "anchorId":'{0}'.format(anchorId),
            "pageNum":'{0}'.format(pageNum),
            "selfTag":"",
            "degree":"1",
        }
        data = urllib.parse.urlencode(formdata).encode(encoding='utf-8')

        request = urllib.request.Request(url, headers=headers, data=data)
        response = urllib.request.urlopen(request)
        text = json.loads(response.read())
        write_txt(text)

        hasNext = text['data']['hasNext']
        anchorId = text['data']['anchorId']
        pageNum += 1

if __name__ == '__main__':
    main()
