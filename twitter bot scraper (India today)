import tweepy
import pandas as pd
import requests
from bs4 import BeautifulSoup
import time
from html.parser import HTMLParser
import datetime as dt




api_key="keys"
api_sec="secret key"
api_bearertoken="b token"
api_token="token"
api_tokensec="token sec"

print(api_key, api_sec, api_bearertoken, api_token, api_tokensec)
auth= tweepy.OAuthHandler(api_key,api_sec)
auth.set_access_token(api_token, api_tokensec )

api=tweepy.API(auth)



url = 'https://www.indiatoday.in/'
response = requests.get(url)
results = BeautifulSoup(response.content, 'html.parser')

results.find_all('article')



# finding all the elements with an <article> tag from html doc of the site
articles = results.find_all('article')  
all_articles = []   

for article in articles:
    
    # Store data for each article in a dictionary 
    dict_article = {}    
    headline = article.find('h2')   
    if headline:
        dict_article['headline'] = headline.text.strip()    
    
    link = article.find('a')   
    if link:    
        dict_article['link'] ="www.indiatoday.in/" + link['href']    
    
    summary = article.find('p')   
    if summary:    
        dict_article['summary'] = summary.text    
    #dict_article['updated_time'] = dt.datetime.now().strftime('%Y-%m-%d %H:%m')   
    
    all_articles.append(dict_article)   
# Convert to a df
df = pd.DataFrame(all_articles)  
print(df.columns)
print(df.head(15))
from nltk import word_tokenize 
import nltk

from nltk.corpus import stopwords
from nltk import FreqDist
#clean text
dim=list(df.shape)

for i in range(dim[0]):
    
    ar=f"{df.loc[i,'headline']}  {df.loc[i,'summary']}"
    print(ar)  

    try:
        
    


        def clean_text(ar):
            if (article is None) or (pd.isna(article)):
                return None
            # Tokenize words in article
            tokens = word_tokenize(ar)
            tokens_flattened = [t.strip() for t in tokens]

            # Return only characters
            tokens_chars = [t.lower() for t in tokens_flattened if t.isalpha()]

            # Remove stop words 
            stop_words = list(set(stopwords.words('english')))
            [stop_words.append(x) for x in ['said', 'says', 'say']]   
            cleaned_tokens = [t for t in tokens_chars if t not in stop_words]
            return cleaned_tokens


            # Calculate frequency of each token
        def get_token_frequencies(cleaned_text, n_tokens=5):
                fdist_tokens = FreqDist(cleaned_text)
                fdist_tokens_sorted = {k: v for k, v in sorted(fdist_tokens.items(), key=lambda x: x[1], reverse=True)[:n_tokens]}

                return fdist_tokens_sorted


        bitlyaccesstoken="fb4ed3ebe7ef1e37f6ba9f788a06f4f65a8b0b21"

        print(df.columns)
        clean=clean_text(ar)
        gettokens=get_token_frequencies(clean, n_tokens=5)
        a=list(gettokens.keys())
        print(clean)
        for item in a:
            print(item)
        str=""
        for tag in a:
            str="#"+tag+" "+str
        api.update_status(f"{df.loc[i,'headline']}\n{df.loc[i,'link']}\n"+str)


    except Exception as e:
        print(f"error:{e}")
        try:
            api.update_status(f"{df.loc[i,'headline']}\n{df.loc[i,'link']}")    
        except Exception as q:
            print(f"error2nd:{e}")

    time.sleep(60)
