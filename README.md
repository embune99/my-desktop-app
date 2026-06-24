# MyDesktopApp

App Electron tối giản để **test tính năng GitHub Release artifacts**. App không có tính năng gì — chỉ mở 1 cửa sổ hiển thị version Electron.

## Chạy local

```bash
npm install
npm start
```

## Build artifacts local (không publish)

```bash
npm run dist      # build cho OS hiện tại, output vào dist/
```

## Test GitHub Release artifacts

Có 2 cách:

### Cách 1 — Tự động qua GitHub Actions (khuyến nghị)

Workflow [.github/workflows/release.yml](.github/workflows/release.yml) sẽ build trên Linux/Windows/macOS và upload artifacts lên GitHub Release khi push 1 tag `v*`:

```bash
# nâng version trong package.json cho khớp tag, rồi:
git tag v0.1.0
git push origin v0.1.0
```

GitHub Actions sẽ tạo một **draft release** kèm các artifacts (AppImage, deb, nsis, dmg, zip...). Vào tab Releases để publish.

### Cách 2 — Publish thủ công từ máy

```bash
export GH_TOKEN=<personal_access_token>   # cần quyền repo
npm run release
```

## Lưu ý

- `publish.owner` / `publish.repo` trong `package.json` đang trỏ tới `embune99/my-desktop-app` — đổi nếu repo khác.
- electron-builder dùng biến môi trường `GH_TOKEN` để upload. Trong CI, `secrets.GITHUB_TOKEN` được cấp sẵn.
- Version trong `package.json` nên khớp với tag (vd tag `v0.1.0` ↔ version `0.1.0`).
