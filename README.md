## Prisma-Schema-Many-to-Many-Relation

```prisma
generator client {
  provider = "prisma-client-js"
  output   = "../app/generated/prisma"
}

datasource db {
  provider = "postgresql"
}

model User {
  id String @id @default(cuid())
  email String @unique
  password String
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  profile Profile? @relation("UserProfile")
  posts Post[]
  comments Comment[]
}

model Profile {
  id String @id @default(cuid())
  firstName String
  lastName String
  city String
  postalCode String
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  userId String @unique
  user User @relation("UserProfile", fields: [userId], references: [id], onDelete: Cascade, onUpdate: Cascade)
}

model Post {
  id String @id @default(cuid())
  title String
  content String
  published Boolean @default(false)
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  authorId String
  author User @relation(fields: [authorId], references: [id], onDelete: Cascade, onUpdate: Cascade)
  comments Comment[]
}

model Comment {
  id String @id @default(cuid())
  content String
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  postId String
  post Post @relation(fields: [postId], references: [id], onDelete: Cascade, onUpdate: Cascade)
  userId String
  user User @relation(fields: [userId], references: [id], onDelete: Cascade, onUpdate: Cascade)
}
```
---

![schema table relational diagram](https://imgur.com/hDLyPeH.png)
##### visit---> https://prisma-editor.bahumaish.com/ --->see relational table diagram.
