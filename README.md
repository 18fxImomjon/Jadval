
<!DOCTYPE html>
<html lang="uz">
<head>
    <title>8-A sinf Dars Jadvali</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            padding: 20px;
        }
        input {
            padding: 5px;
            width: 200px;
            margin-bottom: 10px;
        }
        button {
            padding: 5px 10px;
            cursor: pointer;
        }
        #natija {
            margin-top: 15px;
            font-weight: bold;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        table, th, td {
            border: 1px solid black;
        }
        th, td {
            padding: 8px;
            text-align: center;
        }
        th {
            background-color: #f0f0f0;
        }
    </style>
</head>
<body>

<h1>8-A sinf Dars Jadvali</h1>

<input type="text" id="qidiruv" placeholder="Fan yoki soat: Masalan, Ona tili yoki 5-soat">
<button onclick="qidir()">Qidirish</button>

<div id="natija"></div>

<table>
    <thead>
        <tr>
            <th>Soat</th>
            <th>Dushanba</th>
            <th>Seshanba</th>
            <th>Chorshanba</th>
            <th>Payshanba</th>
            <th>Juma</th>
        </tr>
    </thead>
    <tbody id="jadval">
    </tbody>
</table>

<script>
const darsJadvali = {
    "Dushanba": ["Ona tili", "Robot", "Tarbiya", "Adabiyot", "Algebra", "Geometriya", "IELTS", "-"],
    "Seshanba": ["Informatika", "Rus tili", "Kimyo", "Algebra", "Ona tili", "Geografiya", "Fizika", "Ingliz tili"],
    "Chorshanba": ["Ingliz tili", "Ingliz tili", "Uzb Tarix", "Algebra", "Adabiyot", "Geometriya", "Fizika", "-"],
    "Payshanba": ["Geografiya", "Uzb Tarix", "Algebra", "Informatika", "San'at", "Biologiya", "Fizika", "IELTS"],
    "Juma": ["M.soati", "Geometriya", "Jahon", "Rus tili", "Kimyo", "Ingliz tili", "Biologiya", "Jismoniy"]
};

// Jadvalni chizish funksiyasi
function jadvalniChiz() {
    const jadvalTbody = document.getElementById('jadval');
    jadvalTbody.innerHTML = '';

    for (let i = 0; i < 8; i++) {
        let row = <tr><td>${i + 1}-soat</td>;
        for (let kun of ["Dushanba", "Seshanba", "Chorshanba", "Payshanba", "Juma"]) {
            row += <td>${darsJadvali[kun][i]}</td>;
        }
        row += '</tr>';
        jadvalTbody.innerHTML += row;
    }
}

// Qidirish funksiyasi
function qidir() {
    const qidiruvMatni = document.getElementById('qidiruv').value.trim().toLowerCase();
    const natijaDiv = document.getElementById('natija');

    if (!qidiruvMatni) {
        natijaDiv.innerHTML = '<p style="color:red;">Iltimos, fan yoki soat kiriting!</p>';
        return;
    }

    // Fanga ko‘ra qidirish
    let natijaText = '';
    let topildi = false;

    for (let kun in darsJadvali) {
        darsJadvali[kun].forEach((fan, index) => {
            if (fan.toLowerCase() === qidiruvMatni) {
                natijaText += <li>${kun} - ${index + 1}-soat</li>;
                topildi = true;
            }
        });
    }

    // Soatga ko‘ra qidirish
    const soatRaqami = parseInt(qidiruvMatni.replace('soat', '').trim());
    if (!isNaN(soatRaqami) && soatRaqami >= 1 && soatRaqami <= 8) {
        natijaText = <h3>${soatRaqami}-soat darslari:</h3><ul>;
        for (let kun in darsJadvali) {
            natijaText += <li>${kun}: ${darsJadvali[kun][soatRaqami - 1]}</li>;
        }
        natijaText += '</ul>';
        topildi = true;
    }

    if (!topildi) {
        natijaText = <p style="color:red;">Hech narsa topilmadi!</p>;
    } else {
        natijaText = <h3>Natijalar:</h3><ul> + natijaText + </ul>;
    }

    natijaDiv.innerHTML = natijaText;
}

// Boshlang‘ich chizish
jadvalniChiz();
</script>
<p style="color: red; text-align: center; margin-top: 20px; font-size: 20px; font-weight: bold; font-family: Arial, sans-serif;">
    Created by Imomjon
</p>
</body>
</html>
