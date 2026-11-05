<div align="center">

# 🍇 Blox Fruit Monitor

### Hệ thống lưu trữ kho đồ & giám sát tài khoản Blox Fruit tự động

[![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?style=for-the-badge&logo=node.js&logoColor=white)](https://nodejs.org)
[![Express](https://img.shields.io/badge/Express-4.x-000000?style=for-the-badge&logo=express&logoColor=white)](https://expressjs.com)
[![Discord](https://img.shields.io/badge/Discord-Webhook-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.com)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
[![Version](https://img.shields.io/badge/Version-6.0.0-blue?style=for-the-badge)]()

**Lưu trữ kho đồ • Heartbeat • Phát hiện offline • Báo cáo Discord**

[Tính năng](#-tính-năng) • [Cài đặt](#-cài-đặt) • [Cấu hình](#%EF%B8%8F-cấu-hình) • [API](#-api-endpoints) • [Triển khai](#-triển-khai) • [FAQ](#-faq)

</div>

---

## 📋 Mục lục

- [Giới thiệu](#-giới-thiệu)
- [Tính năng](#-tính-năng)
- [Kiến trúc hệ thống](#-kiến-trúc-hệ-thống)
- [Yêu cầu hệ thống](#-yêu-cầu-hệ-thống)
- [Cài đặt](#-cài-đặt)
- [Cấu hình](#%EF%B8%8F-cấu-hình)
- [Sử dụng](#-sử-dụng)
- [API Endpoints](#-api-endpoints)
- [Triển khai](#-triển-khai)
- [Cấu trúc dự án](#-cấu-trúc-dự-án)
- [Bảo mật](#-bảo-mật)
- [Troubleshooting](#-troubleshooting)
- [FAQ](#-faq)
- [Đóng góp](#-đóng-góp)
- [License](#-license)

---

## 🎯 Giới thiệu

**Blox Fruit Monitor** là hệ thống backend Node.js kết hợp với script Roblox cho phép bạn:

- 📦 **Lưu trữ kho đồ** Blox Fruit lên cloud (JSON storage)
- 💓 **Giám sát hoạt động** tài khoản qua cơ chế heartbeat
- 🔴 **Phát hiện offline** tự động khi mất kết nối
- 📊 **Báo cáo chi tiết** về Discord với phân loại (Trái / Kiếm / Võ thuật / Súng)
- 🟢 **Thông báo online lại** khi tài khoản kết nối trở lại

Dữ liệu được lưu **an toàn** trên server riêng của bạn, không phụ thuộc bên thứ ba.

---

## ✨ Tính năng

### 📦 Lưu trữ kho đồ
- ✅ Lưu toàn bộ inventory (tên + số lượng) lên server
- ✅ Phân loại tự động: **Trái**, **Kiếm**, **Võ thuật**, **Súng**, **Khác**
- ✅ Auto-backup (5 bản gần nhất) — chống corrupt
- ✅ Atomic write — không bao giờ mất dữ liệu giữa chừng
- ✅ Truy vấn kho đồ qua REST API

### 💓 Giám sát hoạt động
- ✅ Heartbeat mỗi **60 giây** (cấu hình được)
- ✅ Phát hiện offline sau **3 phút** không ping
- ✅ Báo cáo tự động khi mất kết nối đột ngột
- ✅ Báo cáo ngay khi nhấn phím `P` (disconnect chủ động)
- ✅ Thông báo "online trở lại" khi kết nối lại

### 📊 Discord Notification
- ✅ Embed đẹp, phân loại theo màu
- ✅ Chống spam (`offlineNotified` flag)
- ✅ Auto-retry khi rate limit (429)
- ✅ Queue system — không bị mất tin nhắn
- ✅ Chia nhỏ embed khi kho đồ lớn (>10 embeds)

### 🛡️ Bảo mật & Độ tin cậy
- ✅ Header `X-Secret` bắt buộc cho write operations
- ✅ Game Guard — chỉ chạy trên Blox Fruit thật
- ✅ Graceful shutdown (SIGTERM/SIGINT)
- ✅ Error recovery khi DB corrupt
- ✅ Path traversal & injection safe

---

## 🏗️ Kiến trúc hệ thống
