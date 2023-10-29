# bike-sharing-demand

## 概要
バイクシェアリングシステムとは、会員登録からレンタル、返却までが自動化された自転車レンタルシステムです。このシステムを利用することで、人々は1つの場所で自転車を借り、必要に応じて別の場所に返却することができる。現在、世界中に500以上の自転車シェアリング・プログラムがある。

これらのシステムによって生成されるデータは、移動時間、出発場所、到着場所、経過時間が明確に記録されるため、研究者にとって魅力的なものとなっている。したがって、バイクシェアリング・システムはセンサー・ネットワークとして機能し、都市におけるモビリティの研究に利用することができる。このコンペティションでは、参加者は、ワシントンD.C.のキャピタル・バイクシェア・プログラムにおける自転車レンタル需要を予測するために、過去の利用パターンと天候データを組み合わせることが求められる。

## eda

### eda001
データの中身確認

### eda002
countの分布を確認

### eda003
datetimeを年、月、日、時、曜日に分割

### eda004
年、月、日、時、曜日ごとのcountとの関係を確認\
全体の相関を確認

### eda005
hourごとのholiday, workingday, dayofweekとcountの関係を確認

### eda006
weatherとcountの関係を確認

### eda007
temp, atempとcountの関係を確認\
temp, count, その他特徴量で散布図を見てみた

### eda008
humidityとcountの関係を確認

### eda009
exp003で作った特徴量を使って相関を確認

## exp

### exp001
datetimeを抜いてLightGBMで学習\
validation score: 1.3144342441425931\
private score: 1.31429\
public score: 1.31429\
あまり変わらないので過学習していないと思う

### exp002
kfold=5で学習\
validation score: 1.2931299603117299

### exp003
datetimeを年、月、日、時、曜日に分割して活用\
learning_rate=0.01に下げた\
validation score: 0.42527243059731556\
private score: 0.49256\
public score: 0.49256\
ちょっと過学習気味？0.07の差をどう見ればいいのかわからない\
特徴量的には、EDAしていた通り、hourは重要な特徴量だった\
その他、year, workingday, temp, atempも重要な特徴量だった\
次はOptuna使って最適なパラメータを探そうかな

### exp004
countを対数変換して学習\
validation score: 0.28487622196889606\
private score: 0.3978\
public score: 0.3978\
leaderboardだと207位で良い感じ\
やはりeda002通り、countの分布的に対数変換するのが良いみたい\
ただ、validation scoreとprivate scoreに乖離があるので、過学習している可能性はあるなと\