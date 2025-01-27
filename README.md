# **โครงสร้างของ GitHub Pages** ขึ้นอยู่กับวิธีที่คุณต้องการใช้งาน GitHub Pages และประเภทของโฮสต์ที่คุณตั้งค่าไว้ โดยทั่วไป GitHub Pages มีการทำงานในลักษณะต่อไปนี้

---

## **1. ประเภทของ GitHub Pages**

GitHub Pages มี 3 ประเภทหลัก:

1. **User/Organization Pages (เพจส่วนบุคคล/องค์กร)**

   - โฮสต์ผ่านโดเมน `username.github.io`
   - ต้องสร้างรีโพสิทอรีชื่อ **`username.github.io`** (เช่น `johnsmith.github.io`)
   - เนื้อหาจะถูกโฮสต์โดยอัตโนมัติจาก **branch `main` หรือ `master`**

2. **Project Pages (เพจของโปรเจ็กต์)**

   - โฮสต์ผ่านโดเมน `username.github.io/repository-name`
   - สามารถสร้างเพจในรีโพสิทอรีใด ๆ โดยใช้ branch `gh-pages` หรือกำหนดเองผ่าน **GitHub Pages settings**

3. **Organization Pages (เพจขององค์กร)**
   - ลักษณะการทำงานเหมือน User Pages แต่ใช้กับองค์กรแทน

---

## **2. โครงสร้างไฟล์ GitHub Pages**

โครงสร้างของไฟล์สำหรับ GitHub Pages มักจะประกอบด้วย:

`/my-repo (ชื่อโปรเจ็กต์)
│-- index.html        # หน้าแรกของเว็บไซต์
│-- about.html        # หน้าข้อมูลเพิ่มเติม (ถ้ามี)
│-- 404.html          # หน้า error 404 (ถ้ามี)
│-- README.md         # เอกสารประกอบโครงการ (ไม่แสดงในหน้าเว็บ)
│-- assets/           # โฟลเดอร์สำหรับไฟล์ CSS, JS, รูปภาพ
│   ├── css/
│   │    └── styles.css
│   ├── js/
│   │    └── script.js
│   ├── images/
│   │    └── logo.png
│-- docs/             # ไฟล์เอกสาร (ถ้ามี)
│-- _config.yml       # การตั้งค่า (ใช้กับ Jekyll)
│-- CNAME             # สำหรับใช้กำหนดโดเมนแบบกำหนดเอง`

### **รายละเอียดไฟล์หลัก**

1. **`index.html`** – หน้าเว็บหลักที่ GitHub Pages จะโหลดโดยอัตโนมัติ
2. **`README.md`** – ไฟล์ Markdown ที่แสดงคำอธิบายใน GitHub repository (ไม่มีผลต่อเว็บไซต์)
3. **`_config.yml`** – ใช้ตั้งค่าหากใช้ Jekyll เช่น การตั้งค่า theme, plugin
4. **`CNAME`** – กำหนดโดเมนแบบกำหนดเองแทน `username.github.io`
5. **`404.html`** – หน้าแสดงข้อผิดพลาดเมื่อ URL ไม่ถูกต้อง

---

## **3. การใช้งาน GitHub Pages**

### **วิธีสร้าง GitHub Pages แบบง่าย**

1. สร้าง repository ใหม่ใน GitHub
2. เพิ่มไฟล์ `index.html`
3. ไปที่ **Settings > Pages** ใน repository
4. ในส่วน **"Branch"**, เลือก branch ที่ต้องการ (`main` หรือ `gh-pages`)
5. คลิก **"Save"** – ระบบจะสร้างเว็บไซต์ให้โดยอัตโนมัติ

### **วิธีใช้ GitHub Pages กับ Jekyll (Static Site Generator)**

1. เพิ่มไฟล์ `_config.yml` และใช้ theme ที่รองรับ
2. ใช้โครงสร้างไฟล์เช่น:
   `/_layouts/
/_includes/
/_posts/
/_site/  (ผลลัพธ์ของการ build)`
3. Push ไฟล์ไปยัง GitHub และ GitHub จะ build เว็บไซต์ให้โดยอัตโนมัติ

---

## **4. การปรับแต่ง GitHub Pages**

- ใช้ **Jekyll Themes** โดยระบุใน `_config.yml` เช่น:
  `yaml
theme: minima
`
- สร้างหน้าเว็บด้วย **Markdown** โดยสร้างไฟล์ `.md` และ GitHub Pages จะ render อัตโนมัติ
- ใช้ CSS และ JavaScript เพื่อทำให้เว็บดูสวยงามขึ้น

---

## **5. การเผยแพร่และดูเว็บไซต์**

- เมื่อเผยแพร่สำเร็จ คุณสามารถเข้าถึงเว็บไซต์ผ่าน:
  - `https://username.github.io/`
  - หรือ `https://username.github.io/repository-name/` (สำหรับ project pages)
- ในการอัปเดตเว็บ แค่ push การเปลี่ยนแปลงไปยัง branch ที่กำหนด

---

## **6. การใช้ GitHub Actions สำหรับการ Deploy อัตโนมัติ**

ถ้าต้องการปรับแต่งขั้นสูง สามารถใช้ **GitHub Actions** เพื่อ deploy เว็บไซต์อัตโนมัติ เช่น การใช้งานกับ frameworks อย่าง Vue.js, React, หรือ Next.js

ตัวอย่าง workflow:

```yaml
name: Deploy to GitHub Pages
on:
  push:
    branches:
      - main
jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Build Project
        run: npm install && npm run build
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
```

---

## **7. การใช้โดเมนแบบกำหนดเอง**

หากต้องการใช้โดเมนส่วนตัวกับ GitHub Pages:

1. ไปที่ **Settings > Pages > Custom Domain**
2. เพิ่มไฟล์ `CNAME` ไปยัง repo โดยระบุชื่อโดเมนของคุณ
3. ตั้งค่า DNS โดยชี้ `A Record` และ `CNAME Record` ไปยัง GitHub

ตัวอย่างไฟล์ `CNAME`:

`mycustomdomain.com`

---

หวังว่านี่จะช่วยให้คุณเข้าใจการทำงานของ GitHub Pages ได้ดียิ่งขึ้น!
