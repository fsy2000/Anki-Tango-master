# Anki-Tango-master

自动生成可导入 [Anki](https://github.com/ankitects/anki) 的日语单词本（TXT 格式，使用**制表符**分隔字段）。单词本内容取自小学馆的《日中辞典》。

环境需求：python、pykakasi 库。

## 用法

先准备好要生成的单词列表，每行一个。打开 generate.py，将单词列表输入，在最后一行后写一行 “\END”，按回车键。例如：

~~~bash
请输入单词（输入\END结束）：
弾く
服
朝
木
机
起きる
\END
~~~

程序会自动生成一个 **wordlist.txt** 文件，内容是每个单词**三个字段**（单词、发音、释义）的单词本：

~~~
弾く	 ひく	弹;［弦で］拉;［かきならす］弹奏;［つまびく］弹拨.<br>バイオリンを弾く／拉小提琴.<br>琴を弾く／弹琴.<br>
服	 ふく	衣服;西服.<br>子供服／儿童服;童装.<br>婦人服／女装;女服.<br>作業服／劳动服;工作服.<br>服を着る／穿衣服.<br>服を脱ぐ／脱衣服.<br>
朝	 あさ	（1）朝,早晨.<br>朝になる／天亮; 到了早晨.<br>朝早くから夜おそくまで働く／起早睡晚地劳动.<br>あの人は朝が早い／他早晨起得早.<br>朝がつらい／早晨懒得起来.<br>（2）〔午前〕早上;午前.<br>仕事は朝何時からですか／工作早上几点钟开始?<br>朝は8時からです／午前八点钟开始.<br>『比較』“早晨”は夜明けから8朝9時までの早朝.ときに夜12時から昼12時までもさす.“早上”は広く朝をいう.<br>
木	 き	（1）〔樹木〕树,树木.<br>3本の松の木／三棵松树.<br>木の幹／树干.<br>木のしん／树心.<br>木の節／树节子.<br>木の実／树上结的果实.<br>木のやに／树脂.<br>木の陰／树阴影;树阴.<br>木の切り株／树伐倒后的残株.<br>木に止まっている鳥／落在树上的鸟儿.<br>木になっている果実／树上结的果实.<br>木に登る／爬树;上树.<br>木を植える／植树.<br>木を切る／伐树;砍树.<br>木を見て森を見ず／见树不见林.<br>（2）〔材木〕木头,木材,木料.<br>木で造った家／用木材盖的房子; 木造房.<br>（3）〔拍子木〕梆子.<br>
机	 つくえ	桌子;［読書・書きもの用］书桌,书案';［事務用］办公桌;［書きもの用］写字台;［長方形の］案.<br>丸い机／圆桌.<br>片袖机／一头沉桌子.<br>机に向かって仕事をする／坐在桌前工作;伏案工作.<br>机を並べて共に働く／并着桌子一同工作.▼郵便局などで客が記入するための机を“写字台”という。“案”は単独では用いない.<br>机の虫 书呆子.<br>
起きる	 おきる	（1）〔立ちあがる〕起,起来,立起来;坐起来.<br>倒れていた稲が起きた／倒伏的稻子立起来了.<br>むっくと起きる／蓦地站起来;猛然站起来.<br>起きて食べなさい／坐起来吃吧.<br>（2）〔ねどこをはなれる〕起床.<br>朝5時に起きる／早晨五点钟起床.<br>朝起きてから夜寝るまで／从早晨起床到晚间睡觉; 从早到晚.<br>病人はまもなく起きられるでしょう／病人不久就能够起床了.<br>（3）〔めざめている〕不睡 .<br>夜遅くまで起きてこつこつ勉強する／孜孜不倦地学习到深夜.<br>起きている間はたいていこの仕事をしている／除了睡觉,我大部分时间从事这项工作.<br>（4）〔事件などが〕发生.<br>困ったことが起きた／发生了一件麻烦事.<br>事件が起きないとも限らぬ／说不定会发生事件.⇒おこる（起こる）<br>
~~~

打开 Anki，点击导入文件，注意要勾选 “允许在字段中使用HTML” 选项，如图：

![导入文件](./README/导入文件.png)

新版本的 Anki 可能会默认使用逗号分割字段，这时需要修改成制表符，如图：

![制表符](./README/制表符.png)

Anki 默认的卡片类型中没有三个字段的，可以自定义一个新的卡片类型。依次点击添加 → 类型 → 管理 → 添加，就能添加自定义的卡片类型。具体可以查阅 Anki 的教程。

## 分离例句和释义

由于词典上是将例句和义项杂糅在一起的，每个义项下就会显示这个义项的例句。如果想将释义和例句分离成两个字段，可以运行 rearrange.py 程序，它会自动读取当前目录下的 wordslist.txt 文件并重整例句，生成一个 **wordslist2.txt** 文件，内容为单词、发音、释义、例句的**四字段**单词本。

~~~
弾く	 ひく	弹;［弦で］拉;［かきならす］弹奏;［つまびく］弹拨.<br>	<b>バイオリンを弾く</b><br>　拉小提琴.<br><b>琴を弾く</b><br>　弹琴.<br>
服	 ふく	衣服;西服.<br>	<b>子供服</b><br>　儿童服;童装.<br><b>婦人服</b><br>　女装;女服.<br><b>作業服</b><br>　劳动服;工作服.<br><b>服を着る</b><br>　穿衣服.<br><b>服を脱ぐ</b><br>　脱衣服.<br>
朝	 あさ	（1）朝,早晨.<br>（2）〔午前〕早上;午前.<br>	<b>朝になる</b><br>　天亮; 到了早晨.<br><b>朝早くから夜おそくまで働く</b><br>　起早睡晚地劳动.<br><b>あの人は朝が早い</b><br>　他早晨起得早.<br><b>朝がつらい</b><br>　早晨懒得起来.<br><b>仕事は朝何時からですか</b><br>　工作早上几点钟开始?<br><b>朝は8時からです</b><br>　午前八点钟开始.<br>『比較』“早晨”は夜明けから8朝9時までの早朝.ときに夜12時から昼12時までもさす.“早上”は広く朝をいう.
木	 き	（1）〔樹木〕树,树木.<br>（2）〔材木〕木头,木材,木料.<br>（3）〔拍子木〕梆子.<br>	<b>3本の松の木</b><br>　三棵松树.<br><b>木の幹</b><br>　树干.<br><b>木のしん</b><br>　树心.<br><b>木の節</b><br>　树节子.<br><b>木の実</b><br>　树上结的果实.<br><b>木のやに</b><br>　树脂.<br><b>木の陰</b><br>　树阴影;树阴.<br><b>木の切り株</b><br>　树伐倒后的残株.<br><b>木に止まっている鳥</b><br>　落在树上的鸟儿.<br><b>木になっている果実</b><br>　树上结的果实.<br><b>木に登る</b><br>　爬树;上树.<br><b>木を植える</b><br>　植树.<br><b>木を切る</b><br>　伐树;砍树.<br><b>木を見て森を見ず</b><br>　见树不见林.<br><b>木で造った家</b><br>　用木材盖的房子; 木造房.<br>
机	 つくえ	桌子;［読書・書きもの用］书桌,书案';［事務用］办公桌;［書きもの用］写字台;［長方形の］案.<br>	<b>丸い机</b><br>　圆桌.<br><b>片袖机</b><br>　一头沉桌子.<br><b>机に向かって仕事をする</b><br>　坐在桌前工作;伏案工作.<br><b>机を並べて共に働く</b><br>　并着桌子一同工作.▼郵便局などで客が記入するための机を“写字台”という。“案”は単独では用いない.<br>机の虫 书呆子.
起きる	 おきる	（1）〔立ちあがる〕起,起来,立起来;坐起来.<br>（2）〔ねどこをはなれる〕起床.<br>（3）〔めざめている〕不睡 .<br>（4）〔事件などが〕发生.<br>	<b>倒れていた稲が起きた</b><br>　倒伏的稻子立起来了.<br><b>むっくと起きる</b><br>　蓦地站起来;猛然站起来.<br><b>起きて食べなさい</b><br>　坐起来吃吧.<br><b>朝5時に起きる</b><br>　早晨五点钟起床.<br><b>朝起きてから夜寝るまで</b><br>　从早晨起床到晚间睡觉; 从早到晚.<br><b>病人はまもなく起きられるでしょう</b><br>　病人不久就能够起床了.<br><b>夜遅くまで起きてこつこつ勉強する</b><br>　孜孜不倦地学习到深夜.<br><b>起きている間はたいていこの仕事をしている</b><br>　除了睡觉,我大部分时间从事这项工作.<br><b>困ったことが起きた</b><br>　发生了一件麻烦事.<br><b>事件が起きないとも限らぬ</b><br>　说不定会发生事件.⇒おこる（起こる）<br>
~~~

例句和释义分离后的显示效果（内含我自定义的 CSS 样式）：

![截图](./README/截图.png)
