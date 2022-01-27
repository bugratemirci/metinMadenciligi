# Metin Madenciliği

## Veri Önişleme

1. Tokenization
+ Metnin boşluk, -- vb sembollerle istenen özelliklere göre parçalara ayrılması işlemidir. Bu parçaların her birine `token` denir. Bu parçaların her biri token dizisi içine atılır.

```
tokenizer = new natural.TreebankWordTokenizer();
console.log(tokenizer.tokenize("my dog hasn't any fleas"));

\\ ['my', 'dog', 'has','n\t', 'any', 'fleas']

tokenizer = new natural.RegexpTokenizer({pattern: /\-/});
console.log(tokenizer.tokenize("flea-dog"));
// [ 'flea', 'dog' ]

tokenizer = new natural.WordPunctTokenizer();
console.log(tokenizer.tokenize("my dog hasn't any fleas."));
// [ 'my',  'dog',  'hasn',  '\'',  't',  'any',  'fleas',  '.' ]

tokenizer = new natural.OrthographyTokenizer({language: "fi"});
console.log(tokenizer.tokenize("Mikä sinun nimesi on?"));
// [ 'Mikä', 'sinun', 'nimesi', 'on' ]
```
2. Remove Unused Words/Chars
+ `Stop Words:` Metinde geçen ve, veya, the, at, and gibi kelimelerin modelin doğruluğunu bozmaması için atılması işlemi.
+ `Digits:` Metinde geçen rakamların atılması.
+ `InvalidCharacters:` Unicode olarak ifade edilemeyen, tanımlanamayan karakterlerin atılması.

+ `Newlines:` \n yeni satır vb (\t\r) gibi karakterlerin silinmesi.

3. Normalization Words
+ `Lowercase/UpperCase:` Metin içerisindeki kelimelerin tek tip bir büyüklüğe getirilmesi.
+ `Trim:` Kelimenin etrafındaki boşlukların silinmesi işlemi, yapılmasının sebebi kelimeleri saf halleriyle kullanılabilir hale getirmek.


# String Distance

1. `Hamming Mesafesi:` bilgisayar bilimlerinde aynı uzunluktaki iki dizgi (string) arasında, birbirine dönüşmesi için gerekli olan yer değiştirme sayısını verir. Yani basitçe bir dizginin diğer dizgiden ne kadar farklı olduğunu gösterir.
```
console.log(hamming('foo','fao'))

// 1
```
2. `Jaro–Winkler Distance: ` (Benzeyen Karakter Toplamı / Toplam Karakter)
```
console.log(natural.JaroWinklerDistance('peter', 'petra'));

// 0.9066666666666667
```
3. `Levenshtein Distance: `Kelimeyi kaç karakter değişimi ile diğer kelimeye benzetebileceğimizi verir.
```
console.log(natural.LevenshteinDistance('peter', 'peter'));

// 0
```
# Bag of Words
+ Bag of Words: Metnin karakterini verecek çeşitli nicelikler hesaplayabiliriz. Kelime çantasında kullanılan en yaygın özellik terim sıklığıdır. 
1. Can film seyretmeyi sever. Meryem de filmleri sever.
2. Can futbol maçı seyretmeyi de sever.
Bu iki metin belgesine dayanarak şöyle bir liste oluşturulur:
```-
[
    "Can",
    "film",
    "futbol",
    "maçı",
    "seyretmeyi",
    "sever",
    "Meryem",
    "de",
    "filmleri"
]

[1, 1, 0, 0, 1, 2, 1, 1, 1]
[1, 0, 1, 1, 1, 1, 0, 1, 0]
```

# TF-IDF
+ Bir terimin doküman içerisindeki önemini gösteren istatistiki yöntem ile hesaplanmış ağırlık faktörüdür.

`TF:` Terim sıklığı, metinde ya da veri kümesinde bulunan her kelimenin kaç kez geçtiğini yakalar, bir kelimenin belgedeki görünme sıklığını ölçer. Örneğin, bir makalede “seo” kelimesi 10 defa geçiyorsa ve makalenin tamamı 500 kelimeden oluşuyorsa TF değeri 0,02’dir (10/500).

`IDF:` IDF bize kelimenin belge için ne kadar önemli olduğunu söyler. Bu, o kelimenin tüm belge setinde ne kadar yaygın veya nadir olduğu anlamına gelir. 0’a ne kadar yakınsa, kelime o kadar yaygındır. İncelenen tüm belgelerin adedi 10 ise ve test edilen anahtar kelime, külliyattaki üç belgede görünüyorsa, bu durumda IDF değeri 0.52’dir (log (10/3)).

