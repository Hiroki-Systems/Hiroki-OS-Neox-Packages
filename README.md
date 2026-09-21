# HirokiOS Pacman/Muz deposu

Bu başlangıç deposu boş bir Arch uyumlu paket deposudur. Paket eklemek için
`x86_64/` klasörüne `*.pkg.tar.zst` dosyalarını
koyup `repo-add` ile veritabanını yeniden oluşturun.

## Config örneği (imzasız test deposu)

Bu başlangıç paket deposu imzasız test içindir. Muz config dosyasına şunu
ekleyin:

```ini
[HirokiOS]
SigLevel = Never
Server = https://OWNER.github.io/REPO/$arch
```

`SigLevel = Never` yalnızca kendi GitHub hesabınız ve test makineniz için
kullanılmalıdır. Bu ayarda GitHub deposuna paket koyabilen veya bağlantıyı
değiştirebilen biri root olarak paket kurdurabilir.

## Paket ekleme

```sh
cp hiroki-desktop-*.pkg.tar.zst x86_64/
cd x86_64
repo-add hiroki.db.tar.gz *.pkg.tar.zst
cp -f hiroki.db.tar.gz hiroki.db
cp -f hiroki.files.tar.gz hiroki.files 2>/dev/null || true
```

`.pkg.tar.zst` dosyası `x86_64/` içine konur; GitHub Actions workflow'u
veritabanını otomatik günceller. GPG anahtarı, `.sig` dosyası ve Actions secret
gerekmez.

Aynı paket adıyla daha yüksek `pkgver` veya `pkgrel` yayınlandığında Muz/Pacman
kurulu eski sürümü yeni sürümle günceller.
