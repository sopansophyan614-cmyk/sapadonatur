# Coding Rules Firebase Firestore

Salin dan tempel aturan berikut ke tab **Rules** pada **Firestore Database** di Firebase Console, lalu klik **Publish**.

## Opsi A: Mode Tim Internal (Tanpa Login)

Cocok digunakan langsung oleh tim internal tanpa layar login, dengan validasi struktur field dasar agar data donatur dan riwayat pesan tetap rapi:

```javascript
rules_version = '2';

service cloud.firestore {
  match /databases/{database}/documents {
    match /donors/{donorId} {
      allow read: if true;
      allow create, update: if request.resource.data.keys().hasAll(['id', 'nama', 'no_wa'])
                            && request.resource.data.nama is string
                            && request.resource.data.no_wa is string;
      allow delete: if true;
    }

    match /message_history/{msgId} {
      allow read: if true;
      allow create: if request.resource.data.keys().hasAll(['id', 'donor_id', 'message', 'sent_at'])
                    && request.resource.data.message is string;
      allow update, delete: if false;
    }

    match /{document=**} {
      allow read, write: if false;
    }
  }
}
```

## Opsi B: Mode Produksi dengan Firebase Auth (Direkomendasikan untuk Publik)

Jika aplikasi sudah dilengkapi fitur login (Firebase Authentication), gunakan aturan ini agar hanya pengguna yang terautentikasi yang dapat membaca dan menulis data:

```javascript
rules_version = '2';

service cloud.firestore {
  match /databases/{database}/documents {
    match /donors/{donorId} {
      allow read, write: if request.auth != null;
    }

    match /message_history/{msgId} {
      allow read, create: if request.auth != null;
      allow update, delete: if false;
    }

    match /{document=**} {
      allow read, write: if false;
    }
  }
}
```
