# Personal Portfolio Website Brief

## Problem

Saya membutuhkan website portofolio pribadi yang sederhana untuk memperkenalkan profil profesional, pengalaman, project, dan cara menghubungi saya.

Website ini juga akan digunakan sebagai project pilot untuk menguji workflow planning menggunakan OpenCode + Superpowers.

## Objective

Membuat website portofolio statis yang:

- sederhana;
- responsif;
- mudah dibaca;
- dapat dijalankan tanpa backend;
- dapat disimpan di GitHub;
- mudah dipublish melalui GitHub Pages atau layanan static hosting lainnya.

## Target Users

Pengunjung utama:

- kolega profesional;
- mahasiswa;
- calon kolaborator;
- recruiter;
- partner freelance;
- orang yang melihat profil dari LinkedIn atau GitHub.

## Required Sections

Website minimal memiliki:

1. Hero
   - nama;
   - professional title;
   - deskripsi singkat;
   - tombol menuju project dan contact.

2. About
   - profil singkat;
   - area expertise;
   - minat profesional.

3. Experience
   - pengalaman kerja atau akademik;
   - role;
   - periode;
   - deskripsi singkat.

4. Projects
   - minimal 3 project;
   - nama project;
   - deskripsi;
   - teknologi;
   - link repository jika tersedia.

5. Skills
   - technical skills;
   - tools;
   - bidang expertise.

6. Contact
   - email;
   - GitHub;
   - LinkedIn.

7. Footer.

## Functional Requirements

FR-01
Website harus memiliki navigasi menuju setiap section.

FR-02
Navigasi harus menggunakan smooth scrolling.

FR-03
Website harus responsif pada desktop dan mobile.

FR-04
Project card harus memiliki link menuju repository GitHub.

FR-05
Contact section harus memiliki link eksternal yang dapat diklik.

FR-06
Tidak menggunakan backend atau database.

## Non-Functional Requirements

NFR-01
Website harus dapat dijalankan langsung sebagai static website.

NFR-02
Tidak menggunakan framework berat untuk versi pertama.

NFR-03
Struktur source code harus mudah dipahami.

NFR-04
Website harus memiliki semantic HTML.

NFR-05
CSS harus terorganisasi dan tidak berlebihan.

NFR-06
JavaScript hanya digunakan jika memang diperlukan.

## Preferred Stack

Gunakan:

- HTML5
- CSS3
- Vanilla JavaScript

Hindari untuk versi pertama:

- React
- Next.js
- database
- authentication
- backend API

## Visual Direction

Tampilan yang diinginkan:

- clean;
- professional;
- modern;
- minimal;
- typography yang mudah dibaca;
- whitespace cukup;
- tidak terlalu banyak animasi.

Gunakan satu accent color secara konsisten.

## Initial File Structure

Ini hanya proposal awal dan boleh direvisi melalui brainstorming.

```text
personal-portfolio/
├── index.html
├── css/
│   └── style.css
├── js/
│   └── main.js
├── assets/
│   └── images/
├── README.md
└── BRIEF.md
```
