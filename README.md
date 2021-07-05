# elasticsearch-japanese-full-text-search
elasticsearch japanese full text search

## nornal serch
### post data
POST _bulk 
{"index": {"_index": "my_suggest"}}
{"my_field": "AAA_AAA"} 
{"index": {"_index": "my_suggest"}}
{"my_field": "AAA_AAB"} 
{"index": {"_index": "my_suggest"}}
{"my_field": "AAA_AAC"} 
{"index": {"_index": "my_suggest"}}
{"my_field": "AAA_BAA"} 
{"index": {"_index": "my_suggest"}}
{"my_field": "AAA_BBA"} 
{"index": {"_index": "my_suggest"}}
{"my_field": "AAB_AAA"} 
{"index": {"_index": "my_suggest"}}
{"my_field": "AAB_AAB"} 
{"index": {"_index": "my_suggest"}}
{"my_field": "ABC_AAA"} 
{"index": {"_index": "my_suggest"}}
{"my_field": "BBC_AAA"}
{"index": {"_index": "my_suggest"}}
{"my_field": "BBB_AAA"} 
{"index": {"_index": "my_suggest"}}
{"my_field": "BBB_AAA"} 

### search
POST my_suggest/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "wildcard": {
            "my_field": "*AAB*"
          }
        }
      ]
    }
  }
}

## japanese full text search
### make mapping

PUT my_suggest1
{ 
  "settings": { 
    "analysis": { 
      "char_filter": { 
        "normalize": { 
          "type": "icu_normalizer",
          "name": "nfkc",
          "mode": "compose" 
        },
        "kana_to_romaji": { 
          "type": "mapping",
          "mappings": [ 
            "あ=>a",
            "い=>i",
            "う=>u",
            "え=>e",
            "お=>o",
            "か=>ka",
            "き=>ki",
            "く=>ku",
            "け=>ke",
            "こ=>ko",
            "さ=>sa",
            "し=>shi",
            "す=>su",
            "せ=>se",
            "そ=>so",
            "た=>ta",
            "ち=>chi",
            "つ=>tsu",
            "て=>te",
            "と=>to",
            "な=>na",
            "に=>ni",
            "ぬ=>nu",
            "ね=>ne",
            "の=>no",
            "は=>ha",
            "ひ=>hi",
            "ふ=>fu",
            "へ=>he",
            "ほ=>ho",
            "ま=>ma",
            "み=>mi",
            "む=>mu",
            "め=>me",
            "も=>mo",
            "や=>ya",
            "ゆ=>yu",
            "よ=>yo",
            "ら=>ra",
            "り=>ri",
            "る=>ru",
            "れ=>re",
            "ろ=>ro",
            "わ=>wa",
            "を=>o",
            "ん=>n",
            "が=>ga",
            "ぎ=>gi",
            "ぐ=>gu",
            "げ=>ge",
            "ご=>go",
            "ざ=>za",
            "じ=>ji",
            "ず=>zu",
            "ぜ=>ze",
            "ぞ=>zo",
            "だ=>da",
            "ぢ=>ji",
            "づ=>zu",
            "で=>de",
            "ど=>do",
            "ば=>ba",
            "び=>bi",
            "ぶ=>bu",
            "べ=>be",
            "ぼ=>bo",
            "ぱ=>pa",
            "ぴ=>pi",
            "ぷ=>pu",
            "ぺ=>pe",
            "ぽ=>po",
            "きゃ=>kya",
            "きゅ=>kyu",
            "きょ=>kyo",
            "しゃ=>sha",
            "しゅ=>shu",
            "しょ=>sho",
            "ちゃ=>cha",
            "ちゅ=>chu",
            "ちょ=>cho",
            "にゃ=>nya",
            "にゅ=>nyu",
            "にょ=>nyo",
            "ひゃ=>hya",
            "ひゅ=>hyu",
            "ひょ=>hyo",
            "みゃ=>mya",
            "みゅ=>myu",
            "みょ=>myo",
            "りゃ=>rya",
            "りゅ=>ryu",
            "りょ=>ryo",
            "ぎゃ=>gya",
            "ぎゅ=>gyu",
            "ぎょ=>gyo",
            "じゃ=>ja",
            "じゅ=>ju",
            "じょ=>jo",
            "びゃ=>bya",
            "びゅ=>byu",
            "びょ=>byo",
            "ぴゃ=>pya",
            "ぴゅ=>pyu",
            "ぴょ=>pyo",
            "ふぁ=>fa",
            "ふぃ=>fi",
            "ふぇ=>fe",
            "ふぉ=>fo",
            "ふゅ=>fyu",
            "うぃ=>wi",
            "うぇ=>we",
            "うぉ=>wo",
            "つぁ=>tsa",
            "つぃ=>tsi",
            "つぇ=>tse",
            "つぉ=>tso",
            "ちぇ=>che",
            "しぇ=>she",
            "じぇ=>je",
            "てぃ=>ti",
            "でぃ=>di",
            "でゅ=>du",
            "とぅ=>tu",
            "ぢゃ=>ja",
            "ぢゅ=>ju",
            "ぢょ=>jo",
            "ぁ=>a",
            "ぃ=>i",
            "ぅ=>u",
            "ぇ=>e",
            "ぉ=>o",
            "っ=>t",
            "ゃ=>ya",
            "ゅ=>yu",
            "ょ=>yo",
            "ア=>a",
            "イ=>i",
            "ウ=>u",
            "エ=>e",
            "オ=>o",
            "カ=>ka",
            "キ=>ki",
            "ク=>ku",
            "ケ=>ke",
            "コ=>ko",
            "サ=>sa",
            "シ=>shi",
            "ス=>su",
            "セ=>se",
            "ソ=>so",
            "タ=>ta",
            "チ=>chi",
            "ツ=>tsu",
            "テ=>te",
            "ト=>to",
            "ナ=>na",
            "ニ=>ni",
            "ヌ=>nu",
            "ネ=>ne",
            "ノ=>no",
            "ハ=>ha",
            "ヒ=>hi",
            "フ=>fu",
            "ヘ=>he",
            "ホ=>ho",
            "マ=>ma",
            "ミ=>mi",
            "ム=>mu",
            "メ=>me",
            "モ=>mo",
            "ヤ=>ya",
            "ユ=>yu",
            "ヨ=>yo",
            "ラ=>ra",
            "リ=>ri",
            "ル=>ru",
            "レ=>re",
            "ロ=>ro",
            "ワ=>wa",
            "ヲ=>o",
            "ン=>n",
            "ガ=>ga",
            "ギ=>gi",
            "グ=>gu",
            "ゲ=>ge",
            "ゴ=>go",
            "ザ=>za",
            "ジ=>ji",
            "ズ=>zu",
            "ゼ=>ze",
            "ゾ=>zo",
            "ダ=>da",
            "ヂ=>ji",
            "ヅ=>zu",
            "デ=>de",
            "ド=>do",
            "バ=>ba",
            "ビ=>bi",
            "ブ=>bu",
            "ベ=>be",
            "ボ=>bo",
            "パ=>pa",
            "ピ=>pi",
            "プ=>pu",
            "ペ=>pe",
            "ポ=>po",
            "キャ=>kya",
            "キュ=>kyu",
            "キョ=>kyo",
            "シャ=>sha",
            "シュ=>shu",
            "ショ=>sho",
            "チャ=>cha",
            "チュ=>chu",
            "チョ=>cho",
            "ニャ=>nya",
            "ニュ=>nyu",
            "ニョ=>nyo",
            "ヒャ=>hya",
            "ヒュ=>hyu",
            "ヒョ=>hyo",
            "ミャ=>mya",
            "ミュ=>myu",
            "ミョ=>myo",
            "リャ=>rya",
            "リュ=>ryu",
            "リョ=>ryo",
            "ギャ=>gya",
            "ギュ=>gyu",
            "ギョ=>gyo",
            "ジャ=>ja",
            "ジュ=>ju",
            "ジョ=>jo",
            "ビャ=>bya",
            "ビュ=>byu",
            "ビョ=>byo",
            "ピャ=>pya",
            "ピュ=>pyu",
            "ピョ=>pyo",
            "ファ=>fa",
            "フィ=>fi",
            "フェ=>fe",
            "フォ=>fo",
            "フュ=>fyu",
            "ウィ=>wi",
            "ウェ=>we",
            "ウォ=>wo",
            "ヴァ=>va",
            "ヴィ=>vi",
            "ヴ=>v",
            "ヴェ=>ve",
            "ヴォ=>vo",
            "ツァ=>tsa",
            "ツィ=>tsi",
            "ツェ=>tse",
            "ツォ=>tso",
            "チェ=>che",
            "シェ=>she",
            "ジェ=>je",
            "ティ=>ti",
            "ディ=>di",
            "デュ=>du",
            "トゥ=>tu",
            "ヂャ=>ja",
            "ヂュ=>ju",
            "ヂョ=>jo",
            "ァ=>a",
            "ィ=>i",
            "ゥ=>u",
            "ェ=>e",
            "ォ=>o",
            "ッ=>t",
            "ャ=>ya",
            "ュ=>yu",
            "ョ=>yo" 
          ] 
        } 
      },
      "tokenizer": { 
        "kuromoji_normal": { 
          "mode": "normal",
          "type": "kuromoji_tokenizer" 
        } 
      },
      "filter": { 
        "readingform": { 
          "type": "kuromoji_readingform",
          "use_romaji": true 
        },
        "edge_ngram": { 
          "type": "edge_ngram",
          "min_gram":1,
          "max_gram":10 
        },
        "synonym": { 
          "type": "synonym",
          "lenient": true,
          "synonyms": [ 
            "nippon, nihon" 
          ] 
        } 
      },
      "analyzer": { 
        "suggest_index_analyzer": { 
          "type": "custom",
          "char_filter": [ 
            "normalize" 
          ],
          "tokenizer": "kuromoji_normal",
          "filter": [ 
            "lowercase",
            "edge_ngram" 
          ] 
        },
        "suggest_search_analyzer": { 
          "type": "custom",
          "char_filter": [ 
            "normalize" 
          ],
          "tokenizer": "kuromoji_normal",
          "filter": [ 
            "lowercase" 
          ] 
        },
        "readingform_index_analyzer": { 
          "type": "custom",
          "char_filter": [ 
            "normalize",
            "kana_to_romaji" 
          ],
          "tokenizer": "kuromoji_normal",
          "filter": [ 
            "lowercase",
            "readingform",
            "asciifolding",
            "synonym",
            "edge_ngram" 
          ] 
        },
        "readingform_search_analyzer": { 
          "type": "custom",
          "char_filter": [ 
            "normalize",
            "kana_to_romaji" 
          ],
          "tokenizer": "kuromoji_normal",
          "filter": [ 
            "lowercase",
            "readingform",
            "asciifolding",
            "synonym" 
          ] 
        } 
      } 
    } 
  },
  "mappings": { 
    "properties": { 
      "my_field": { 
        "type": "keyword",
        "fields": { 
          "suggest": { 
            "type": "text",
            "search_analyzer": "suggest_search_analyzer",
            "analyzer": "suggest_index_analyzer" 
          },
          "readingform": { 
            "type": "text",
            "search_analyzer": "readingform_search_analyzer",
            "analyzer": "readingform_index_analyzer" 
          } 
        } 
      } 
    } 
  } 
}

### check analyzer
POST my_suggest1/_analyze
{
  "analyzer": "suggest_index_analyzer",
  "text": "日曜日は本部に人が集まる"
}

POST my_suggest1/_analyze
{
  "analyzer": "readingform_index_analyzer",
  "text": "日曜日は本部に人が集まる"
}

### put data

POST _bulk 
{"index": {"_index": "my_suggest1"}}
{"my_field": "日本"} 
{"index": {"_index": "my_suggest1"}}
{"my_field": "日本人"} 
{"index": {"_index": "my_suggest1"}}
{"my_field": "アメリカ人"} 
{"index": {"_index": "my_suggest1"}}
{"my_field": "日米首脳会談"} 
{"index": {"_index": "my_suggest1"}}
{"my_field": "日の本"} 
{"index": {"_index": "my_suggest1"}}
{"my_field": "本屋"} 
{"index": {"_index": "my_suggest1"}}
{"my_field": "日本 地図"} 
{"index": {"_index": "my_suggest1"}}
{"my_field": "日本 　地図"} 
{"index": {"_index": "my_suggest1"}}
{"my_field": "日本の地図"} 
{"index": {"_index": "my_suggest1"}}
{"my_field": "日は本当にまた昇るのか?"} 
{"index": {"_index": "my_suggest1"}}
{"my_field": "日本郵政"} 
{"index": {"_index": "my_suggest1"}}
{"my_field": "日本 郵便"} 
{"index": {"_index": "my_suggest1"}}
{"my_field": "美しい国、日本"} 
{"index": {"_index": "my_suggest1"}}
{"my_field": "日本大使館"} 
{"index": {"_index": "my_suggest1"}}
{"my_field": "日本の人口"} 
{"index": {"_index": "my_suggest1"}}
{"my_field": "日本人の口癖"} 
{"index": {"_index": "my_suggest1"}}
{"my_field": "日本 代表"}
{"index": {"_index": "my_suggest1"}}
{"my_field": "日本人の誇り"} 
{"index": {"_index": "my_suggest1"}}
{"my_field": "日曜日は本部に人が集まる"}
{"index": {"_index": "my_suggest1"}}
{"my_field": "焼肉"}
{"index": {"_index": "my_suggest1"}}
{"my_field": "焼き肉"}
{"index": {"_index": "my_suggest1"}}
{"my_field": "焼きにく"}
{"index": {"_index": "my_suggest1"}}
{"my_field": "ヤキニク"}

### search

GET my_suggest1/_search 
{ 
  "size":20,
  "query": { 
    "bool": { 
      "should": [
        {
          "match": { 
            "my_field.suggest": { 
              "query": "日曜日は本部に人が集まる" 
            } 
          } 
        },
        { 
          "match": { 
            "my_field.readingform": { 
              "query": "日曜日は本部に人が集まる",
              "fuzziness":"AUTO",
              "operator": "or" 
            } 
          } 
        } 
      ] 
    } 
  }
}
