# Git Kullanım Rehberi

### Örnek

Bir projeniz olduğunu varsayalım: C++ ile hesap makinası yapıyorsunuz. Bu bir C++ eğitimi olmadığı için kodları minimum seviyede tutma amacıyla header vs gibi detayları yazmayacağız.

**hesapmak** klasöründe main.cpp dosyanızın şöyle bir içeriği olduğunu düşünün:

```c++
void main() {
    printf("Hello Git!");
}
```

Şimdi bu uygulamanızı Git ile takip edebilmeniz için hesapmak klasöründe bir git repo'su oluşturmalısınız. Terminalinizde hesapmak klasörüne gidip bu komutu çalıştırın:

```
git init
```

Artık bu klasördeki tüm dosyalar git ile takip edilebilir haldeler. Fakat henüz takip edilmiyorlar!

Şimdi `git status` komutu çalıştırın.

![enter image description here][1]

**git** main.cpp dosyamızı gördü ama *Untracked* yani henüz takip edilmiyor. Yani sadece çalışma alanımız (Working Directory) içerisinzde . Şimdi Git'e "Bu dosyaya takip et!" dememiz, yani Staging Area'ya almamız gerekiyor.

```
git add main.cpp
```

Tekrardan repomuzun durumuna bakalım.

![enter image description here][2]

Artık git bu dosyamızı takip ediyor ve bize diyor ki; **Bu dosyada bazı değişiklikler var ama henüz commit edilmemiş**. Hemen commit işlemini gerçekleştirelim.

```
git commit -m 'bu benim commit mesajım'
```

![enter image description here][3]

Tebrikler! İlk commitiniz başarıyla sonuçlandı! :) Git `main.cpp` dosyanızın o anki halini kaydetti. Şimdi `main.cpp` dosyanızda rastgele değişiklikler yapın. Diyelim ki bazı değişiklikler yaptınız, birşeyler denediniz ama istediğiniz sonuçları alamadınız. Kodunuz çalışmıyor, töbe yarabbi acayip acayip birşeyler oldu. TÜm değişiklikleri silip son çalışır haline yani en son commitinizdeki haline geri döndürmek istiyorsunuz. Önce bir `git status` diyerek hangi dosyalarda değişiklik var, ne olmuş ne bitmiş bir bakalım.

![enter image description here][4]

**main.cpp** değiştirilmiş ama henüz commit edilmemiş. Biz bu değişiklikleri hemen geri alalım. `git status` komutu bize bunu nasıl yapacağımızı da söylüyor zaten. (Ekran görüntüsü 5. satır)

```
git checkout -- main.cpp
```

Şimdi `main.cpp` dosyanızı açtğınızda yaptığınız değişikliklerin gittiğini ve dosyanın son committeki haline döndüğünü göreceksiniz. Tekrar `git status` diyerek kontrol edebilirsiniz. Şimdi `main.cpp`'de tekrar değişiklikler yapın ve diyelim ki bu değişiklikler canavar gibi çalışıyor ve dosyanın bu halini saklamak istiyorsunuz. Tekrar `git status` ile kontrol edebilirsiniz. Dosyayı yine `git add main.cpp` ile commit edilecekler listesine ekliyoruz ve daha sonra commit ediyoruz.

![enter image description here][5]

Farkettiyseniz dosyanın sadece çalışır ve memnun olduğumuz hallerini commit ettik. Bu nokta çok önemli. **Her zaman dosyalarınızın nihai, çalışır hallerini commit edin.** 

Dosyanızda hangi tarihte ne değişiklikler yaptığınızı merak ederseniz istediğiniz commite geri dönebilirsiniz. Bunun için önce commitlerimizi listeleyelim.

```
git log
```

![enter image description here][6]

Şimdi bakalım ilk committen sonra ne değişiklikler olmuş? Commitin ID'sini (Benimki 801a... diye gidiyor, sizinki farklı olacaktır.)

```
git diff 801a786096c84596ff13a1f86759cc99d4ef1607
```

![enter image description here][7]

Gördüğünüz gibi, ilk commitimde `main.cpp` dosyası boştu ve ben daha sonra ilk satıra **asdasd** yazmışım. 

İlk committeki haline geri dönmek istediğiniz varsayalım.

```
git checkout 801a786096c84596ff13a1f86759cc99d4ef1607
```

Artık `main.cpp` ilk committeki haline döndü. Tekrar en son committeki haline geri döndürmek için aynı komutu kullanabilir ya da kısaca `git checkout master` diyebilirsiniz. Aslında manası daha derin olsa da şimdilik `master`'ın son commitinizi ifade ettiğini söyleyebilirim.

**Editör Notu**

Burada bir hatam oldu ve daha anlaşılır olsun diye commit mesajlarında "İlk mesajım." gibi ifadeler kullandım. Normalde böyle anlaşılmaz mesajlar gönderdiğinizde çalışma arkadaşlarınızdan dayak yiyebilirsiniz. Çünkü bu mesajlar çok önemli. Mesajlarda her zaman o committe ne değişiklik yaptığınızı, hangi bug'ı düzelttiğiniz yazmalısınız ki yarın öbür gün "ben hangi committe şu hatayı düzeltmiştim yahu?!" diye debelenmeyin. Birkaç commit mesajı örneği vermek gerekirse :

"Kullanıcıdan veri talep edilen fonksiyon yazıldı."
"Artık scanf yerine cin kullanılıyor."
"Kullanıcının sayı yerine harf girmesi engellendi."
"15 nolu bug düzeltildi."

[1]: http://cl.ly/image/1j1d0E0b273C/Image%202014-08-13%20at%203.39.05%20%C3%96S.png
[2]: http://cl.ly/image/3F3i3a1j3i13/Image%202014-08-13%20at%203.42.10%20%C3%96S.png
[3]: http://cl.ly/image/3Z3u13282Y3b/Image%202014-08-13%20at%203.44.20%20%C3%96S.png
[4]: http://cl.ly/image/2L0l1l0i1p0p/Image%202014-08-13%20at%203.47.20%20%C3%96S.png
[5]: http://cl.ly/image/1f1k1r103v3C/Image%202014-08-13%20at%203.53.55%20%C3%96S.png
[6]: http://cl.ly/image/2O3L1X2v3R3k/Image%202014-08-13%20at%203.57.53%20%C3%96S.png
[7]: http://cl.ly/image/0r2m3O0D2y3c/Image%202014-08-13%20at%204.00.51%20%C3%96S.png
