jma-eqarea-centroid
======

Centroid List of Earthquake Information Area from JMA(Japan Meteorological Agency)  

[気象庁が電文などで使用する区域名](http://www.data.jma.go.jp/svd/eqev/data/joho/shindo-name.html)・区域コードと、その区域の重心(緯度,経度)を対応づけたリストです。  
気象庁防災情報XML電文の**震度速報**、**震源・震度に関する情報**などから得られる区域別の震度(数値)情報を、地図上の当該区域の上にマッピングしたりできます。

震度観測点のリストは更新頻度が高い(おおよそ3〜4回/年)ため当リポジトリには含めていません。必要な場合は [@9SQ/jma-intensity-stations](https://github.com/9SQ/jma-intensity-stations) を実行することで生成できます。

### ファイル

* jma\_area\_centroid.csv : 地震情報／細分区域レベル(188区域)
* jma\_city\_centroid.csv : 気象・地震・火山情報／市町村等レベル(1898区域)

### フォーマット

**CSV**  

```
区域コード,区域名,緯度,経度
```

改行コード : \\n (LF, 0x0A)  
経度緯度の測地系 : WGS84(EPSG:4326)

## 生成に使用したデータ
* [国土交通省 国土数値情報(行政区域 第2.2版)](http://nlftp.mlit.go.jp/ksj/gml/datalist/KsjTmplt-N03.html)  
National Land Numerical Information(Administrative Zones Data Version 2.2), MLIT Japan  
平成26年度 (作成時点:平成26年4月1日)  


* [気象庁防災情報XMLフォーマット 技術資料](http://xml.kishou.go.jp/tec_material.html)  
JMA Disaster Prevention Information XML format Technical Document, JMA  
個別コード表(平成27年4月30日一部更新)   
地震火山関連コード表.xls -> シート24
「AreaForecastLocalE・AreaInformationCity・PointSeismicIntensityコード表」

## データの生成手法

PostgreSQLとPostGIS、QGISを用いて生成  
詳細はこちら  
http://eleclog.quitsq.com/2015/06/postgis-mlit-ksj.html  
http://eleclog.quitsq.com/2015/06/postgis-eqarea-centroid.html

## 特記事項

1. 2014年5月に栃木県下都賀郡岩舟町が栃木市に編入合併されたが、国土数値情報では岩舟町のままなので、気象庁側に合わせて栃木県栃木市に統合後、重心計算を実行
2. 気象庁のデータでは、長崎県佐世保市と長崎県佐世保市宇久島、鹿児島県薩摩川内市と鹿児島県薩摩川内市甑島が別区域扱いになっているので、気象庁側に合わせて別区域として重心計算を実行
