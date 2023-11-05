# Next 14

## 資料夾結構

![strutures](https://nextjs.org/_next/image?url=%2Flearn%2Fdark%2Flearn-folder-structure.png&w=1920&q=75&dpl=dpl_BwAwEtN7ncXAnnwFzTiU7xDupY2g)

1. /app: 主要的資料夾
2. /app/lib: 放hooks, utils
3. /app/ui: UI 元件
4. /public: 圖片 靜態資源
5. /scripts/: 資料庫
6. global.css: reset.css 全域 css 規則
7. 條件判斷的 css 可用 clsx 套件
8. 字型 font.ts
9. 圖片 < Image> 元件
10. 如果要優化 外部圖片 or 本地字型 [看這篇最下面](https://nextjs.org/learn/dashboard-app/optimizing-fonts-images)

## 路由

1. 巢狀路由
   ![image.png](https://hackmd.io/_uploads/BJFgokHQa.png)

2. 以 page.tsx 為主軸，例如 /dashboard/page.tsx => 頁面 /dashboard
3. /dashboard 中所有 page 的共用元件，則放在 /dashboard/layout.tsx，dashboard 的子頁面時，共用元件就不需要 re-render ([partial-rendering](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#3-partial-rendering))
4. < Link> 元件 切換頁面時有 SPA 的效果，而且在載入 Link 元件時，會同步 prefetch 他的對應頁面，達到效能優化的效果。
5. usePathname 或任何 react 的 hook 都需要在 'use client' 環境使用
6. 可以使用 clsx 套件做 active 的樣式
```
'use client';
 
import {
  UserGroupIcon,
  HomeIcon,
  DocumentDuplicateIcon,
} from '@heroicons/react/24/outline';
import Link from 'next/link';
import { usePathname } from 'next/navigation';
import clsx from 'clsx';
 
// ...
 
export default function NavLinks() {
  const pathname = usePathname();
 
  return (
    <>
      {links.map((link) => {
        const LinkIcon = link.icon;
        return (
          <Link
            key={link.name}
            href={link.href}
            className={clsx(
              'flex h-[48px] grow items-center justify-center gap-2 rounded-md bg-gray-50 p-3 text-sm font-medium hover:bg-sky-100 hover:text-blue-600 md:flex-none md:justify-start md:p-2 md:px-3',
              {
                'bg-sky-100 text-blue-600': pathname === link.href,
              },
            )}
          >
            <LinkIcon className="w-6" />
            <p className="hidden md:block">{link.name}</p>
          </Link>
        );
      })}
    </>
  );
}
```


