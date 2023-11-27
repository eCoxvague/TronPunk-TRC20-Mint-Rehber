# TronPunk-TRC20-Mint-Rehber

Basılmış olan punkları https://github.com/TronPunks/TronPunks/blob/main/mints.json burdan giderek mints.json dosyasından kontrol edebilirsiniz.

<img width="1334" alt="Ekran Resmi 2023-11-27 19 20 28" src="https://github.com/eCoxvague/TronPunk-TRC20-Mint-Rehber/assets/100167495/d95449e8-fdfd-44ae-b237-ef9bfc7ce906">


Burdaki id'leri alıp mints.json dosyasında arayın yoksa basabilirsiniz. 
Basılan üstüne sizde basarsanız kopya olur bir işe yaramaz dikkatli olun.

Anlatacağım olay node üstünden olacak eğer başka yollarla basmak isteyen olursa https://github.com/TronPunks/TronPunks/blob/main/README.md buraya gidip bakabilir.

---

1. `Node.js` kurulumunu yapın.

2. `TronPunks` adında masaüstüne dosya oluşturun.
   
<img width="121" alt="Ekran Resmi 2023-11-27 19 26 18" src="https://github.com/eCoxvague/TronPunk-TRC20-Mint-Rehber/assets/100167495/023d4b98-ef18-45f8-aaf4-0c0d4b7271ae">


3. Visual Studio Code üstünde oluşturduğumuz klasörü açın.
   
<img width="1020" alt="Ekran Resmi 2023-11-27 19 27 41" src="https://github.com/eCoxvague/TronPunk-TRC20-Mint-Rehber/assets/100167495/64b5852a-254c-47e8-9d1c-5d3910c3560b">


4. Daha sonra Visual üstünde terminali açın ve `npm init` komutunu çalıştırın. Burda çıkanlara `enter` diyerek geçiyoruz herhangi bir bilgi değiştirmiyoruz.
  
<img width="604" alt="Ekran Resmi 2023-11-27 19 38 53" src="https://github.com/eCoxvague/TronPunk-TRC20-Mint-Rehber/assets/100167495/ae58f05f-47c9-40bf-a151-6ed1f9fafc28">


5. Visual üstündeki terminalde `npm install tronweb` kodunu çalıştırıyoruz ve yüklenmesini bekliyoruz.
   
<img width="413" alt="Ekran Resmi 2023-11-27 19 40 46" src="https://github.com/eCoxvague/TronPunk-TRC20-Mint-Rehber/assets/100167495/cd419518-f32e-49ca-aca6-6afd90c5519f">


6. Visual üstünde sol tarafta boş bir yere sağ tık yapıyoruz `yeni dosya` oluştur diyip dosyanın adını `index.js` yapıyoruz. Aşağıdaki kodu bu index.js içine yapıştırıyoruz.
   
<img width="210" alt="Ekran Resmi 2023-11-27 19 41 36" src="https://github.com/eCoxvague/TronPunk-TRC20-Mint-Rehber/assets/100167495/23250aeb-23a2-4e7d-872f-fbee207c1c48">


```
const TronWeb = require('tronweb');
const HttpProvider = TronWeb.providers.HttpProvider;
const fullNode = new HttpProvider("https://api.trongrid.io");
const solidityNode = new HttpProvider("https://api.trongrid.io");
const eventServer = new HttpProvider("https://api.trongrid.io");
const privateKey = "your privateKey"; //
const tronWeb = new TronWeb(fullNode, solidityNode, eventServer, privateKey);

const blackHole = "T9yD14Nj9j7xAB4dbGeiX9h8unkKHxuWwb";  //black hole address

const memo = 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAAkElEQVR42mNgGAWjAAT+f+v7jw3TzGCqWUKMBWRbQsjQdd2JlFmCyyCYGAxTxQJkw5D5ZFuAy7XYMEUWwAwJqDEGY2SDYWJUsQAkFNvtjGIBTGxwBxEpFpBkCT4LQNIUWYArUxHjA7J9AbMkXpYTjinKZOh24XI9SI4qpTW2sKeW4Sg+gBpKVcMZaOlyqlgAAF9AOnOqpdBpAAAAAElFTkSuQmCC';  

async function main() {

    const unSignedTxn = await tronWeb.transactionBuilder.sendTrx(blackHole, 1); //0.000001 TRX is the minimum transfer amount.
    const unSignedTxnWithNote = await tronWeb.transactionBuilder.addUpdateData(unSignedTxn, memo, 'utf8');
    const signedTxn = await tronWeb.trx.sign(unSignedTxnWithNote);
    console.log("signed =>", signedTxn);
    const ret = await tronWeb.trx.sendRawTransaction(signedTxn);
    console.log("broadcast =>", ret);
}

main().then(() => {

    })
    .catch((err) => {
        console.log("error:", err);
    });
```
7. Yapıştırdığımız kodun içinde aşağıdaki resimde gösterdiğim yerleri değiştirin.
    - const privateKey = " "; //
    - const memo = " "; 
  - Tırnak içlerindeki silip " " olacak şekilde değişimleri yapın ve kaydetmeyi unutmayın.
   Kaydetmek için ctrl s yada yukardan file save diyebilirsiniz.

<img width="676" alt="Ekran Resmi 2023-11-27 19 44 18" src="https://github.com/eCoxvague/TronPunk-TRC20-Mint-Rehber/assets/100167495/18c2ebfa-f73c-4193-94a4-8bebfd723cbf">

8. const memo kısmını https://tronpunks.github.io/TronPunks/ burdan giderek mintlemek istedeğiniz NFT'nin üstüne bastıktan sonra çıkan kodu kullanacaksınız.

   <img width="575" alt="Ekran Resmi 2023-11-27 19 52 26" src="https://github.com/eCoxvague/TronPunk-TRC20-Mint-Rehber/assets/100167495/b722f07b-ac22-4095-9d0c-3d544415ee53">


9. Bütün işlemleri yapıp kaydettikten sonra terminal kısmına `node index.js` kodunu yazıp mint işlemini gerçekleştiriyoruz.
    - Giden fee 1.5 tron civarında bilginiz olsun.


<img width="756" alt="Ekran Resmi 2023-11-27 19 54 32" src="https://github.com/eCoxvague/TronPunk-TRC20-Mint-Rehber/assets/100167495/68505b41-1bd7-4b4a-a466-79575edbab0e">
