# rollup.jsでReactのビルド環境を作成した後、Viteを導入して開発用サーバーを導入する

## はじめに

既存のWeb環境に後からReactとViteを導入するという状況を想定して開発環境を作成します

* rollup.jsのビルド環境を作り、簡易Webサーバーで動作確認を行う
* Viteを導入して開発用サーバーで動作確認を行う

通常はViteを導入後、必要があればrollup.jsのビルド環境を整えますが順番を逆にします

### ReactでCounterコンポーネントを作成する
```bash
npm i react react-dom
npm i -D @types/react @types/react-dom typescript
```




### rollup.jsでReactのビルド環境を作成する

```bash
npm i -D rollup tslib @rollup/plugin-typescript @rollup/plugin-commonjs @rollup/plugin-node-resolve @rollup/plugin-replace
```

rollup.config.js

```js:rollup.config.js
import resolve from '@rollup/plugin-node-resolve';
import commonjs from '@rollup/plugin-commonjs';
import replace from '@rollup/plugin-replace';
import typescript from '@rollup/plugin-typescript';

export default {
  input: 'src/lib.ts', // ビルドのエントリーポイント
  output: [
    {
      // esmodule
      file: 'dist/bundle.esm.js', // 出力ファイル名
      format: 'esm',
      sourcemap: true,
    },
  ],
  plugins: [
    peerDepsExternal(),
    resolve(),
    commonjs(),
    replace({
      'process.env.NODE_ENV': JSON.stringify(process.env.NODE_ENV),
      preventAssignment: true,
    }),
    typescript({
      tsconfig: 'tsconfig.app.json',  // TypeScriptの設定(viteの設定ファイルを読み込む)
      compilerOptions: { // 上記設定ファイルから一部設定を変更する
        outDir: "dist",
        declaration: true,　// 型定義ファイルを作成する
        declarationDir: "dist",
        allowImportingTsExtensions: false,
      },
      exclude : [ // 対象外ファイル
        "node_modules",
        "dist",
        "build",
        "src/main.tsx",
        "src/App.tsx",
      ]
    }),
  ],
};
```

Counter.tsx

```
```

App.tsx

```
```
