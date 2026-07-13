# README.md
```markdown
# 最小生成树 MST 算法实现
## 项目简介
本仓库使用纯 C 语言实现两种经典贪心最小生成树算法：
1. Kruskal 克鲁斯卡尔算法（基于边数组 + 并查集，适合稀疏图）
2. Prim 普里姆算法（基于邻接矩阵，适合稠密图）

测试统一无向图：5 个顶点，包含 7 条带权边，两种算法计算出的最小生成树总权值均为 6。

### 专业术语中英对照
- Algorithm：算法
- Minimum Spanning Tree(MST)：最小生成树
- Vertex：顶点
- Edge：边
- Weight：权值
- Greedy algorithm：贪心算法
- Union-Find：并查集
- Adjacency Matrix：邻接矩阵
- Sparse graph：稀疏图（点多、边少）
- Dense graph：稠密图（点少、边多）

## 项目目录结构
```
kruskal与prim算法/
├─ kruskal/
│  ├─ kruskal.h     // 头文件：边结构体、宏、函数声明
│  ├─ kruskal.c     // Kruskal算法、并查集、边排序实现
│  └─ kruskalmain.c // 程序入口 main 函数
├─ prim/
│  ├─ prim.h        // 头文件：邻接矩阵图结构体、宏、函数声明
│  ├─ prim.c        // Prim算法、建图函数实现
│  └─ primmain.c    // 程序入口 main 函数
├─ .gitignore       // Git忽略缓存、可执行文件
└─ README.md        // 项目说明文档
```

## 算法核心思路
### 1. Kruskal 克鲁斯卡尔
1. 把所有边按权值从小到大排序；
2. 依次选取最短边，使用并查集判断两点是否连通；
3. 不连通则加入生成树，连通则跳过（防止出现环路）；
4. 选取 `顶点数-1` 条边后，全部顶点连通，算法结束。

### 2. Prim 普里姆
1. 固定起点顶点，维护一个已连通集合；
2. 每次从集合向外寻找一条权值最小的边，把新顶点并入集合；
3. 使用 lowCost 数组实时更新未选点到集合的最短距离；
4. 所有顶点全部加入连通集合，算法结束。

## 编译 & 运行教程（MinGW gcc）
### 1. 切换到对应算法文件夹
```powershell
# 进入 Kruskal 文件夹
cd kruskal
# 进入 Prim 文件夹
cd prim
```

### 2. 完整编译命令
```powershell
# Prim 编译
gcc primmain.c prim.c -o prim.exe -mconsole -fexec-charset=GBK -g
# Kruskal 编译
gcc kruskalmain.c kruskal.c -o kruskal.exe -mconsole -fexec-charset=GBK -g
```
参数说明：
- `-mconsole`：强制控制台程序，避免 `WinMain` 链接报错；
- `-fexec-charset=GBK`：解决中文输出乱码；
- `-g`：生成调试符号，支持 gdb 断点调试。

### 3. 运行程序
```powershell
.\prim.exe
.\kruskal.exe
```

## 头文件规范说明
所有 `.h` 头文件使用标准头文件保护，防止重复引入报错：
```c
#ifndef PRIM_H
#define PRIM_H
// 宏、结构体、函数声明
#endif
```
- `#ifndef / #define / #endif` 组合避免重复定义；
- 宏统一全大写，区分普通变量。

## 注意事项
1. 编译仅需要填写 `.c` 文件，`.h` 通过 `#include` 自动引入，无需写进 gcc 命令；
2. 不可单独编译 `prim.c` / `kruskal.c`，缺少 `main()` 入口，必须搭配 `xxxmain.c`；
3. `.exe`、`.vs` 缓存文件已配置 `.gitignore`，无需上传至 GitHub；
4. 仓库多人共用推荐使用 `git push revert HEAD` 撤回错误提交；单人仓库可使用 `git push --force-with-lease` 彻底删除错误提交记录。

## 两种算法对比
| 对比项 | Kruskal | Prim |
|--------|---------|------|
| 核心思路 | 全局选最短边 | 连通集合向外抓取最近点 |
| 存储结构 | 边数组 | 邻接矩阵 |
| 核心工具 | 并查集 | lowCost 最小权数组 |
| 最优场景 | 稀疏图（点多边少） | 稠密图（点少边多） |
| 循环次数 | 全部边排序遍历 | 顶点循环遍历 |
```

## 使用操作
1. 本地打开 `README.md`，全选清空原有内容；
2. 把上面整块代码完整复制粘贴进去，保存；
3. 终端推送更新：
```powershell
git add README.md
git commit -m "修复md语法，完整项目说明文档"
git push origin main
```
4. GitHub 页面按 `Ctrl + F5` 强制刷新，即可正常渲染完整格式。