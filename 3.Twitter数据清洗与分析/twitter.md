# 如何利用API查询推特数据



你将会使用 Tweepy （ http://www.tweepy.org/ ）来查询推特 API，以获取 WeRateDogs 推特档案以外的附加数据，包括转发用户和喜欢用户。<br/>



推特 API 要求用户得到授权之后才能使用。这意味着在你运行 API查询代码前，你需要配置好自己的推特应用。在此之前，你必须登录推特账户。
<br/>


这份指南（ https://www.slickremix.com/docs/how-to-get-api-keys-and-tokens-for-twitter/ ）描述了配置过程。
<br/>
一旦完成配置，以下代码将创建一个 API 对象，用于收集推特数据。
<br/>

import tweepy

consumer_key = 'YOUR CONSUMER KEY'
consumer_secret = 'YOUR CONSUMER SECRET'
access_token = 'YOUR ACCESS TOKEN'
access_secret = 'YOUR ACCESS SECRET'

auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_secret)

api = tweepy.API(auth)

<br/>

推特数据以 JSON 格式存储在 Twitter 上。这个 StackOverflow 答案（ https://stackoverflow.com/questions/28384588/twitter-api-get-tweets-with-specific-id ）已经做出了清晰描述，教你如何利用 Tweepy 通过推特 ID 获取推特 JSON 数据。<br/>

注意，在调用 get_status 后， 请将参数 tweet_mode 设置为 'extended'，即 api.get_status(tweet_id, tweet_mode='extended')，这将会非常有用。<br/>


你还需要注意的是，档案中有少数 ID 对应的推特信息也许已经被删除。Try-except 块也许会对你很有帮助。<br/>


不要在项目提交中包含你的推特 API 密钥和访问令牌（可以用 * 号代替）。<br/>


推特 API 具有速率限制。速率限制用于控制服务器发出或接收流量的速率。<br/>
为了在 WeRateDogs 推特档案中查询所有推特 ID，至少需要 20-30 分钟的运行时间。为了使数据更加整洁，你可以在查询后输出每个推特 ID，并使用定时器编码（ https://stackoverflow.com/questions/7370801/measure-time-elapsed-in-python ）。你也可以在 tweepy.api class （ http://docs.tweepy.org/en/v3.2.0/api.html#API ） 中将参数 wait_on_rate_limit 和 wait_on_rate_limit_notify 设置为 True。<br/>



查询每个推特 ID 后，你将要编写 JSON 数据，并按要求将其存入 tweet_json.txt 文件中，每个推特 JSON 数据占一行。接着你可以逐行读取这个文件，来创建一个 pandas DataFrame 以便在之后进行数据评估和清洗。
你还可以阅读这篇来自 Stack Abuse 的文章，名为使用 Python 在文件中读取和编写 JSON（Reading and Writing JSON to a File in Python）（ https://stackabuse.com/reading-and-writing-json-to-a-file-in-python/ ） ,这对你的深入学习非常有用。

如果你无法访问 Twitter 的话，我们将直接给你提供返回的 Twitter 数据，tweet_json.txt。<br/>