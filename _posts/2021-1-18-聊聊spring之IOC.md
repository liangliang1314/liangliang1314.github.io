---
layout: post
title: "聊聊spring之IOC"
date: 2021-1-18 
description: "聊聊spring之IOC"
tag: spring
--- 

我们知道Spring有两大核心的概念IOC与AOP，今天就来聊聊IOC。至于什么是Spring这里就不做任何说明，请自行百度。只有了解Spring的核心，才能更好的掌握Spring。而且Spring也是面试高频的知识点。

很多人在面试过程中，被问到Spring IOC是什么？心里清楚，就是不知道怎么表达出来。好了废话不多说，接下来看看什么是IOC。


#### IOC定义
    所谓 IoC ，就是由 Spring IoC 容器来负责对象的生命周期和对象之间的关系

#### IOC是什么鬼?
在讲解之前我们得先弄清楚这到底是什么玩意？官方解释：***Ioc—Inversion of Control，即“控制反转”***，其实吧这是一种思想，并不是好大上的什么技术。大家心里想：你这不是废话吗，我都知道是***控制反转***。那么如何更好的理解 ***“控制反转”*** 了。首先看下面几个问题。

* 谁控制谁
* 控制什么
* 为何是反转（有了反转就有正转）
* 反转了哪些

怎么理解这上面几个问题了？

在传统的编程中，我们都是直接在对象的内部中 new 一个我们需要的对象。如下：

```
public class Test {

    private Housing h;

    public Test() {
        this.h = new Housing();
    }
}
```
我们可以想一想这样做带来的缺点是什么？

* 自己手动创建对象
* 维护对象的生命周期
* 对象之间的耦合

我们再想想我们到底是依赖的对象本身还是对象的所提供的服务？也就是说我们所依赖的对象需要我们自己去创建吗？其实我们并不需要关心对象是由谁创建谁管理这些琐事，我们只需要依赖的对象能够提供服务就行，我不管你是怎么来的。

此时IoC就出现了，而IoC是有专门一个容器来创建这些对象，即由Ioc容器来控制对象的创建。IoC好比现在的房源中介平台一样。我只需要把我自己的要求告诉你，你给我提供相应的房源即可。这里我们并不需要去关心平台是如何寻找房源的繁琐过程。

在没有引入IOC的时候，对象直接依赖我们所需要的对象，有了IOC后，我们都是通过Ioc Service Provide来管理两者的依赖关系。你想要什么对象，你只需要跟Ioc Service Provide说一声，哥们给我整一个性感漂亮的对象也是可以的。

<br>

图片摘自Spring揭秘
<br>

![image][ioc]

现在我们在回过头来看看上面的四个问题

1：谁控制谁
    
    谁控制谁？通过上面的列子我们知道在传统的开发模式下，我们依赖的对象需要自己去new创建，管理。而有了IOC后可以交给容器管理，所答案是IOC控制对象。
    

2：控制什么
    
    当然是对象

3：为何是反转（有了反转就有正转）

    因为IOC帮我们管理了对象，我们撒手不管了。所以这是反转。我们自己创建依赖的对象为正转。


4：反转了哪些
    
    所依赖的对象反转了。


参考文章
《http://svip.iocoder.cn/Spring/IoC-intro/》









[ioc]:data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAi0AAAEzCAYAAAD93TMEAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAACSUSURBVHhe7d0LnB11fffxhCRAEsluNtlsLptkk2x2s9lkd7NVwMvjhUpvhvapPC3mabWAF1olaJ/WvmqofdRyqdIKiCm1Qq32qYA8opZLVB6vQEUBS5Vb5SYKRBSIPCSacPHf853Z/57/OfvfnD2b/8zOf+cz/9f7lXNm5pyzmZnzm+/5z5w5MxYsWGAAAACKjtACAACiQGgBAABRILQAAIAoEFoAAEAUCC0AACAKhBYAABAFQgsAAIgCoQUAAESB0AIAAKJAaAEAAFEgtAAAgCgQWgAAQBQILQAAIAqEFgAAEAVCCwAAiAKhBQAARIHQAgAAokBoAQAAUSC0AACAKBBaAABAFAgtAAAgCoQWAAAQBUILAACIAqEFAABEgdACAACiQGgBAABRILQAAIAoEFoAAEAUCC0AACAKhBYAABAFQgsAAIgCoQUAAESB0AIAAKJAaAEAAFEgtAAAgCgQWgAAQBQILQAAIAqEFgAAEAVCCwAAiAKhBQAARIHQAgAAokBoAQAAUSC0AACAKBBaAABAFAgtAAAgCoQWAAAQBUILAACIAqEFAABEgdACAACiQGgBAABRILQAAIAoEFoAAEAUCC0AACAKhBYAABAFQgsAAIgCoQUAAESB0AIAAKJAaAEAAFEgtAAAgCgQWoDItW94mdnyoafNL33EYMTSF73Wu6wAxI3QAkSud/vV3h13mW1+z3e9ywpA3AgtQMTae47x7rRhzOL1R3uXGYB4EVqAiPWcdrl3hw1j1r/lMu8yAxAvQgsQqUVdA2b44ue8O2yYZNks6trsXXYA4kRoASLVfcql3p01qrpPvsS77ADEidACRKits8cM7zzg3VGjanjn/mRZ+ZYhgPgQWoAIrd12oXcnjbHWbrvAuwwBxIfQAkRm4dLVZviivd4dNMbSsmrtWOVdlgDiQmgBItN14tnenTPG1/Xas7zLEkBcCC1ARFoWLzND5z/p3TFjfFpmWna+ZQogHoQWICKrt+7w7pTR2Oqt7/IuUwDxILQAkWhpazeD5+327pCzUj/45pmIk6405vP3GvP4PmOe/4Uxew8Y8x8/8s+blcEPPJosQ9+yBRAHQgsQic7jz/DujLN026MjaaUy/Ofj/nka+fPrjXnm+fQ59vw8DSsP/TS975s/S53Hb/cuWwBxILQAEWhpbTMD5z7o3RFnzQ5v/Jx/+sGceIUxB55LH/8Ptxlz9Eer0373ytp58zBwzgPJsvQtYwDFR2gBIrDiFW/07oTzYIf60HJq5f43HzZm3zNpMFEPyunX1s7zuXvSx974UO34qbTi5ad6lzGA4iO0AEXX0mo2vfdO7w44D3ZwQ8ubKrefHTnko0M99z+Z3tb5Km5w2f10Ov7ML1XHTTUtSy1T77IGUGiEFqDglr/4dd6db17s4IaWWx9Jx33hvuq4K+9Mx7kn2Npg85arq+OKYNmxJ3mXNYBiI7QARdbSYvr/4lbvjjcvdnBDy8+fTce9Y1d13FuvTcfpUJEdp28Jafiz66vjiqD/zFuSZetd5gAKi9ACFFjH8FbvTjdPdnBDy/6R0KKgYsfpsJAGneNix9lvH+26tzquKDq2vMa7zAEUF6EFKLCN7/yqd4ebJzu4oUWHgDR8+q7quKvuTsfp5Fw77t1fTsdpeP+NxrxwZLyc8tnq7anQ96df8S5zAMVFaAEKasmm47w72zyNd50W9aropFsND+ypnoirc1j0rSL3OdTLYofH9hpz+25jHh05Qdedbyos6X+Vd9kDKCZCC1BQvWdc493R5ql+cKe9rRJcFEB0qEjnuOjkXH2ryJ1H1LvyV18z5ruPGfOzynzPVYKNwssX7x87b956t1/tXfYAionQAhRQe8+x3p0sAvr79N/2nmO86wBA8RBagALqOe2KsTtZZKLntMu96wBA8RBagIJZ1DVghi9+zruDRXha1ou6NnvXBYBiIbQABdN9yqXenSuy033yJd51AaBYCC1AgbR19pjhnQe8O1ZkZ3jn/mTZ+9YJgOIgtAAFsnbbhd6dKrK3dtsF3nUCoDgILUBBLFy62gxftM+7Q50Obnkk/QHFV3/cP32qDV+0N1kHvnUDoBgILUBBdJ14jndnGsLZXzfm7p+k11TRbwP98Clj3vtV/7xZ+f6e9Houv/Ev/ulF0HXi2d51A6AYCC1AAbS2LzdbLtjj3ZEeqo/cOnJluMpw3xPpRd70+0Cf/K5//qy89FJjXvVP/mlFMXT+k6Zl8TLvOgIw9QgtQAGsPuFM7040hCd/ngYW9bbYcS++xJjXXVk7X7Ne9A/+8bFbvXWHdx0BmHqEFmCKtS5aYgbP2+3dgYZgf5H50m/7p1v6AcN/350ePtpTCTqfutOYl1xanW6Hs76W/g6RfnvITtOhJw0fv7067n2V+TToPBZdyt8O7g8v/t6njbnpB8bsPZD+btG9T1SnSaO/KQtaFy1t7d51BWBqEVqAKbbyV97u3XmGcp3zg4X6raDt142d5/VXpcFAv4F4VyWAPLU/nf/a71XnscPTlYDx4J6UnXbhzek090cVr78/HfdP/177eBtaFFj0mhrUG6RfjtZhK/v4ifxNWek8/gzvugIwtQgtJbNx40YzPDyMAhn6vXO9O85QXv4xY254KN3h2+Hfflh7fol6OzS8/8b0/gmfTO+rN+W4kW/72MH3Q4d2fgWM4z+RHjqyIeOkkcNQdrCh5caRv+lbj6SHqzSu2b8pKwPnPOBdV5i8vr4+b00CmkFoKRlfMcHUGvr9v/buOEN7y9XVIKBBPSF2mno4xhve8Jl0Hjv88eerj3Pd8Vg6/d1fNubkymM06MRfO90ONrTokJCGd+yqzuOayN+UlYGz7/euKxwaX00CmkFoKRmKR/FkfXionv02kc51sePsYRod3rnt0Vrj9ZTUO/8b6XQdvrGvcdE3q9PtYB//zPPpfd/hKpnI35QVDg+FRd1BKISWkqF4FE/WJ+Lu/Fb6dWN7X98i0qATW+24e0ZOpP2wEzLEvRCcHcYLLbr+ig4PPbbXmG/vTm9vda7JYgf7+Dt/nN7/+kPGHP3RdJz7ehP5m7LAibjhUXcQCqGlZCgexZTlV541/OzZ9PDN955Iw4QG95s+O740MrIyPLAn/cbOT/ZVT6K1z6NhvNAiOplWg3px9BzuNDvYx5+xq/q3/LjyWnqs2/szkb8pC3zlOTzqDkIhtJQMxaOYdEGzrC4u97l7jHn0aWOeez495KKvFX/wG2Ovs3JmJSToUIwO2+jKtd+phJw/uqY63Q4HCy1/c9PITJXh3Btqp9nBffzbK8FFPS56TQWrbz5c+5hGf1NoXFwuG9QdhEJoKRmKR3FleRl/TAyX8c8GdQehEFpKhuJRXNP9BxOLjh9MzA51B6EQWkqG4lFsa7dd6N2hIntrt13gXSc4dNQdhEJoKRmKR7G1dfaY4Z0HvDtVZGd45/5k2fvWCQ4ddQehEFpKhuJRfN2nXOrdsSI73Sdf4l0XCIO6g1AILSVD8Si+RV0DZvji57w7V4SnZb2oa7N3XSAM6g5CIbSUDMUjDj2nXeHdwcbklkfSX3g+2MXg9PVnO/im56HntMu96wDhUHcQCqGlZCgecWjvOda7g50Id9CPCz6+L71WS9ZXkq33/T3ptVV0pVzfdJnS0PL36b/tPcd41wHCoe4gFEJLyVA84tF7xjVjd7QTYAddlO2un6TBRYOuOOubPyv66QD3V5t9prqnpXf71d5lj7CoOwiF0FIyFI94LNl0nHdH24gd7JVnddVZO/zmZWPnl/qr4+YlVGiZ7N+/pP9V3mWPsKg7CIXQUjIUj7hsfOdXvTvbg7GDDS3q8bDD66+qneesr6U9MuqNcZ/j1MpjdUn9fc+kl/5XL83p11an3z3yY4bu7xe9r/JcGnQeywsr9+1g/w7R7w3Zy/Lr8JF+BdoOdh455bPpbw3ptfXDjp+605iXOD/6aIfx/v6J6PvTr3iXOcKj7iAUQkvJUDzi0jG81bvDPRg72LDwx59P7+u3h+zhGjs8fcCYByvhQezj31R53LOVeTU89FNj7n8yva1gYIPLhTen4xQY7OOuvz8dZ3/Q0A7273jzv1YPVT38VPq89r4G+zwKVgormqTDW0/tT6df+73qPHbw/f0T1bHlNd5ljvCoOwiF0FIyFI/ItLSY/jNv8e50x2OH+nNa3F4RO3yxEjTcx8qtj6TTvnBfddyVd6bj7HkxJ3wyva+nPv4T6eEZGy5OujKdxw42tNz8w/T+175fPZxzxR3pOA26Lzf9IL3//hvT+/a19P84buRkYjv4/v6J6N/xrWTZepc5gqPuIBRCS8lQPOKz/MWv8+54x+MO6l1RL4QCgA7Z1M+jXhj3saJv/Gh4x67quLdem45TD4gdd8dj6bh3f9mYkz+T3r7viep0O9jQokNNGv7kC9V51PtiBzvOzucb3lB5Hc1jB9/fPxHLjj3Ju6yRDeoOQiG0lAzFI0ItrWbTe+/07nx97OCeS1LPDr559o+EFgUVO06HhTQoUNhx538jHafDNh+5Nb2tc1TsdDvY17CHnLZfV53nbSPPq8GOUzDSoJ6i2x6tNV4vTjM2veeOZJl6lzUyQd1BKISWkqF4xGnFK97o3QH72GGyoUWHgDR8+q7quKvuTsfp5Fw7Ttdf0eGhx/Ya8+3d6e2tzjVZ7GBfw54b89nKc+m+en523ZuO02Afd8/ISb4fdgKQuNeZscNkQsuKl5/qXcbIDnUHoRBaSobiEaeW1jYzcO6D3p1wPTtMNrSoV8WeB/PAnmrYUE+JvlXkzmsDjnpn9G0fd5od7Gucd9PIiMqg59RJvrZXRYN93I4vjYyoDHp9Pe9P9lVP8PU990QNnPNAsix9yxjZoe4gFEJLyVA84tV5/BneHXE9O0w2tIgO29xeCQsKIzrHRSfn6ltF9fP9jRNEzr2hdpod7GuoZ+XvbkkDiL7yrMM99mvSGtzHnlkJLvar0Xr97zxmzB9dU51uh2ZDS+fx273LFtmi7iAUQkvJUDzi1dLWbgbP2+3dGaOxwQ88mixD37JFtqg7CIXQUjIUj7it3rrDu0NGY6u3vsu7TJE96g5CIbSUDMUjbi2Ll5mh85/07pQxvqHzn0iWnW+ZInvUHYRCaCkZikf8uk4827tjxvi6XnuWd1kiH9QdhEJoKRmKR/wWLl1thi/a6905Yywtq9aOVd5liXxQdxAKoaVkKB7Tw9ptF3p30Bhr7bYLvMsQ+aHuIBRCS8lQPKaHts4eM7zzgHcnjarhnfuTZeVbhsgPdQehEFpKhuIxfXSfcql3R42q7pMv8S475Iu6g1AILSVD8Zg+FnUNmOGLn/PurGGSZbOoa7N32SFf1B2EQmgpGYrH9NJz2uXeHTaMWf+Wy7zLDPmj7iAUQkvJUDyml/aeY7w7bBizeP3R3mWG/FF3EAqhpWQoHtNP7/arvTvtMus9/V+9ywpTg7qDUAgtJUPxmH7aN7zMbPnQ096ddxlpWbRveKl3WWFqUHcQCqGlZCgeAPJG3UEohJaSoXgAyBt1B6EQWkqG4gEgb9QdhEJoKRmKB4C8UXcQCqGlZCgeAPJG3UEohJaSoXgAyBt1B6EQWkqG4gEgb9QdhEJoKRmKB4C8UXcQCqGlZCgeAPJG3UEohJaSoXgAyBt1B6EQWkqG4gEgb9QdhEJoKRmKB4C8UXcQCqGlZCgeAPJG3UEohJaSoXgAyBt1B6EQWkqG4gEgb9QdhEJoKRmKB4C8UXcQCqGlZCgeAPJG3UEohJaSoXgAyBt1B6EQWkqG4gEgb9QdhEJoKRmKB4C8UXcQCqGlZCgeAPJG3UEohJaSoXgAyBt1B6EQWkqG4gEgb9QdhEJoKRmKB4C8UXcQCqGlZCgeAPJG3UEohJaSoXgAyBt1B6EQWkqG4gEgb9QdhEJoKRmKB4C8UXcQCqGlZCgeAPJG3UEohJaSoXgAyBt1B6EQWkqG4gEgb9QdhEJoKRmKB4C8UXcQCqGlZCgeAPJG3UEohJaSoXgAyBt1B6EQWkqG4gEgb9QdhEJoKRmKB4C8UXcQCqGlZCgeAPJG3UEohJaSoXgAyBt1B6EQWkqG4gEgb9QdhEJoKRmKB4C8UXcQCqGlZCgeAPJG3UEohJaSoXgAyBt1B6EQWkqG4gEgb9QdhEJoKRmKB4C8UXcQCqGlZCgeAPJG3UEohJaSoXgAyBt1B6EQWkqG4gEgb9QdhEJoKRmKB4C8UXcQCqGlZCgeAPJG3UEohJaSoXgAyBt1B6EQWkqG4gEgb9QdhEJoKRmKB4C8UXcQCqGlZCgeAPJG3UEohJaSoXgAyBt1B6EQWkqG4gEgb9QdhEJoKRmKB4C8UXcQCqGlZCgeAPJG3UEohJaSoXgAyBt1B6EQWkqG4gEgb9QdhEJoKRmKB4C8UXcQCqGlZCgeAPJG3UEohJaSoXgAyBt1B6EQWkqG4gEgb9QdhEJoKRmKB4C8UXcQCqGlZCgeAPJG3UEohJaSoXgAyBt1B6EQWkqG4gEgb9QdhEJoKRmKB4C8UXcQCqGlZCgeAPJG3UEohJaSoXgAyBt1B6EQWqaxhQsXmu7u7hq2eNSP17y+5wCAZlB3kCVCyzTW0tJiBgYGRgvGeDSP5vU9BwA0g7qDLBFapjn3U8541q1b530sAEwGdQdZIbRMcx0dHd6C4dI8vscCwGRQd5AVQss0p+7XwcFBb9EQTaOLFkBI1B1khdBSAgfrqtU032MA4FBQd5AFQksJLFu2zFs4RNN8jwGAQ0HdQRYILSWgbtihoaExhUPj6KIFkAXqDrJAaCmJ9evXjykeGuebFwBCoO4gNEJLSfi6apcvX+6dFwBCoO4gNEJLSag7dsuWLaOFQ7fpogWQJeoOQiO0lEhvb+9o8dBt3zwAEBJ1ByERWkpE3bK2eNBFCyAP1B2ERGgpkdbW1tHiodu+eQAgJOoOQiK0lIy6Z+miRb2jjjpqzG/B6NyDFStW1Iyr19fXV3Nfv9rLb8qgHnUHoRBaSqazszPhm4Zy8wWUNWvWJIGmfrxVH1r0ddbNmzcn46W9vX10mv203cjixYtrnhPxo+4gFELLRLQuMHO3zzWzbpxlZj4+08yIuM1+araZ9dQsZ0xcTctf60HrQ+vFu77QNAUW9ZLYT8QHo51PT09PQhcKs7fVM+N+M0Tzuq9RT2FIIcU3DRXUnUI1ak8xEFoaqWycs3fNdjZdWlHa7OtmUzwC2bRp05hxS5YsSXpa6se73J4Wt1dF5y40OumS0HIQ1J1CN2rP1CG0NKBU7W6stGK1uadXPvV41hsmTuHEF1p0mGfDhg2j993DROph0aEg+696Vfr7+0cPC1kHCyWElvFRd4rfqD1Tg9DSgLoD3Q2VVqw264ZZ3vWGiVFwUOBwQ4vGbdy4Mektcc9DUCixwcX2sNh/9Rz2ttheFz2P/lU4aUbZz2uh7hS/UXumBqGlgdiPJU/3pvXjW2+YGJ3HovNQbGixIUY9KLqv4GJ7UmxgkUahxYYV+6+Pnk8BxTet7Kg7xW/UnqlBaGnA3UhpxWy+9YbmKLTYHhadlGtDi8YNDg7WBBbRdBtubKhxQ4u9TWiZHHf7phW3+dYdskVoacDdQGnFbL71huYotKxatcq0tbUl921oER3qWbp06eh9UeDQj+EplOi20NMSjrt904rbfOsO2SK0NOBuoLRiNt96Q3PqT8R1e1pEPSk20IhuK7ToPBf1zOi+Tui109X7on/dcfUILeNzt29acZtv3SFbhJYG3A2UVszmW29oji+0qIdFvSc2uCigqMdF47u6upL5bO+KvT6L5lNg0Txr165N7tvnrKdpbo8Oqtztm1bc5lt3yBahpQF3A6UVs/nWG5pTH1rUA6KA4oYO3V60aJHp6OgYHW9Di+6rV0WX8Hcfo69Mu/dFh4x0nowCy8qVK2umIeVu37TiNt+6Q7YILQ24GyitmM233tAc99CP1AeN8SjE6F/N714N19L4+ufyjUMtd/umFbf51h2yRWhpwN1AacVsvvUGxMzdvmnFbb51h2wRWhpwN1BaMZtvvQExc7dvWnGbb90hW4SWBtwNlFbM5ltvQMzc7ZtW3OZbd8gWoaUBdwOlFbP51hsQM3f7phW3+dYdskVoacDdQGnFbL71BsTM3b5pxW2+dYdsEVoacDfQZtvM5/y/HzLz+eZ+V2TW07PMjOfdMQVtv5hhDn/kcHdMLs233oCYudv3ZFqo2pM0as+4zbfukC1CSwPuBtpMW/jFhWbtn6x1xlTbwKsGnHtpUzFZ9451Zt5d85yxaeve3m2Wf3i5M2ZsO+znh5mOj3eYw/Yd5owdv8350Ryz6dc3mVn7qr8me+SDR5reU3pH7zfbDjtwWHJ9D3ecWuv1rabnlB5z2P6J/W3NNt96A2Lmbt/NtmZrj22qBRt+f0NNsGn5SotZ82drRu/72uZf2+zcm2GWXLbEbHh95XnGCU7UHhwKQksD7gbaTJu1d5YZeOWAOfzhsel/vMLRcmOLGfjlAbPgG7Wvq08Q/Sf0m9lPzXbG1jYViFVnrTLdb+ue0CejpR9datb8eW0x6vhYh1lx/gpnTHPNVzj0fxo6dshsPn6z6XtdX42jbj7KmXPyzbfegJi523ezbTK1R631/7Watf+rNuyorihMHPHDI5yxta0mtPxihtl44kYz+PJBs+k1mxIrPlRbU6g9OBSElgbcDbTZNu/OecmbWG3T1k1m429vTGx54ZbR23pDveC2F4w8YkZye+735potx26pdUzt/aUfWzr6mNFWCSs9b+4x7Ze3u2Nrmj5FqXBtOXqLGXrpUHLbFrK+3+1LnlvjrSO+f0TyGPe1xfeppqZwVP7fHf/cYTb+j43Jc9h51Ob+51zT+we9NZ+0DqX51hsQM3f7nkybTO1RYGm/rN30/2Z/rcoHpvpxa9+5tvqcL6o+p3p52na1Jc+nwKPHKjwk96k9CIDQ0oC7gU606VOGpSJx5H1H1nwasW/Umc/MTArH7CdmmyPvPzJ5w9t53DZ7z2zvG9XXFn1mkRl8xaCZ9ZT/TalCoufSmzzxs/TNruLVe3Jt9+zgKwfNEQ+nb/oX3P6C5BCUbqt7d/OvbjY9b+ypKTKi5xp6yZDpObXHDP/SsNl0QqVg/k6loI1QAR149YDZ9BvpeE23rzfZ5ltvQMzc7buZNpnao/tzfjwn6Z1xDw2pdZ7Xmezk3XH1zT6/nnPFBdXekrar28yaHdUeFWoPQiC0NOBuoM029Zj0vKknKQS+wqFCsfjTi5PbOqbb/9/7zcpzViZvfjuvWjOhRcef9cZcvtN/DowtHPX3V71vlWn5evqJyLbBlw2aOY/NSW6vuHCFWfVXq5LbrV8Z242s5n7aUferuoarU2ckRWjzr1SWg3P4qn6eyTTfegNi5m7fk2nN1B61zr/tHJ1m2/zb5ycfgLSzt+/ZeXfMSx6r2+ox0c4/6Wmp/KsemIHjKqFg5LCQNfzCtCZQexACoaUBdwNtph3+6OFm42s3mvl3zE96UAb/22C1O9Xpol3yySWjj9E5K3pz6pi0HZeMn2BoUe+KPmnok4s+NSXfOqpr4xUOFTd9qtKJd3ba0IuHktdO5qsEKR0LVtFY/d7VScFTcVj/h+vNzGfTkOUWDjUVBfspR/TJTkXQHafCZ+efbNNrTkT9uvXN48Pj/HicX4jHudt3s63Z2qPzVfSByQ0tSY9GZSe/+P8uTg4FKcAoWOgDkT0fxO70bShSaHEDUucHO5N/N786HTcda4+7zpAPQksD7gY60aZiobPj9Qmj9/W9ZsFNC8zmX08LwOKrqp9u1r95vVl4vf+QkLpV64/juvfdeW1b9tFlZt32dcntrh1dZvnfje1tsYVCBcqyb3YdolKhOvxH6Ql8+gTlHvude+/cpGtWJwsrIOm59C2BFR9Mu4TrC4fO3Ne/6t7VGfx6rSN+UD3GrOdwQ9tkm15zIurXrW8eHx7nx+P8QjzO3b6baZOpPYs/szi5bUOLAkv/b/UnAUf3dci576S+JJTMvWduMk6tUWhJejb0b11omU61x11nyAehpQF3A51Qez59ky78fKUIvHIgebPPeXxOcvxUbzz7VUR9utFxWx3XtY/VJw59ArCfMGybSE/LnCfmJMex9YlI9494qPL8lU9Y9d8gsIVjvPsKPkn3a+X/ofH1h6oUhvq29Y3e1zFznaGv7mhbOPRv65dbk09a+sSnbzTpk1H36d3J8WT9bUv/cWlS9JZe4jmhuMnmW29AzNzte8JtkrVn5oH0Pa4duw7/KOSseVflQ9NIaFGP7dDLhpL3re7bpp4KnWjrHh6qCS2VkJH826Cnxd6n9mAiCC0NuBvoRJs9gUxvYHV5tn6pNene1Dh9HVBBouvMrjHXXpn/H/OTguGOU2sYWn4xI7nGi3vSm5reuPo2kcKQHdeocKiA6e/XiW/2WLRtyaedSgHqfUOvabs2/YaAmj32bAuHXq/rL7vMkv+zJPkE1X5F+o0Efa1x9XtWJ8VRBeXw3WO/kjmZ5ltvQMzc7buZNtnao6b3pXbyyTcTKzXFhhY1fW1Zh2bsfTV9M6frL7qSHpL535mfBAIbWlQDbC2baGih9mAiCC0NuBtos82+gY/61lFm9V+mb3h10+pNozdS/YXgll28bPSEM7c1Ci0qKPrkUH8dF735dex65ftXjo5rVDhs07cKdEb+6P2fzjb9v91vFl29KCks+vvrz5mxhUMFT8VS/2edmKdiN++eeclJxrp4Vd/v9CXHxw/lugxu8603IGbu9j2Z1mztUdMO3Z4jomZDi967ySGjEyo7/090jEydkYQbhRYdstEXABQMdEKvpulaU+rpURDp/EA6jtqDEAgtDbgbaLPNFo5V56wybdeknw706Udvru63difHVe28ahv+54bkDeeOUxsvtOhNv/IDK5OuYHWVutNs03gdNup6d1dygq8tFPVfFXQfo7bg5gWjXwnU62/YtiH5f9jpOgaubxGoyCXdzJViMf+785MTgTVdn+Tar2xPvhWlblgtC41TsdRJcZpn3dvXmfZPjX9NmYk233oDYuZu35NpzdYeNYUWe1s9FgotOmdEh1V0gUvVkiQI/O/VZsVFK5KvFissJK9Vef+3XZe+js4dUWDRY3VejT1ETe1BCISWBtwNtNmmN4ve7HrT602mTxzqMtUbLPmEUikASy9dmnyyUHdlcvJZ5RPEkn9ZUnPS7Xh0+EfPPV5gsS05Tl15s6pH5mCfdhb824JkPvXO6Ox9HfvVePXgqAC5h5ls0/FxPV50AbxlH1mW9PDo5D4VBv0fdaVeddWqyGi8vSaD/q/q7tXx8+ozNt986w2Imbt9T6Y1U3vsY9zQot4IXetEYcH9NqMOAek9vvLclaO9NTYg6fwZvY56NOwJu+pxUQDRCcLUHoRAaGnA3UCbberS1Nn7OgabXLp6x5qaIqErReoNPu/u9NoH+s0OO20iTZ+W1HXqjhuv6ROL7frV8efqlPSTkf7ViW9HPnBk8vc0c8xXv+uRfOIZuQaCipF6gPSJSNN07FuFTce+daEq9/eVNK97Vv9kmm+9ATFzt+/JtGZqjx1ng4KaelDsV5sbNT2//p31/2clX7HWe7o6Nb1mjOqPblN7cKgILQ24GyitmM233oCYuds3rbjNt+6QLUJLA+4GSitm8603IGbu9k0rbvOtO2SL0NKAu4HSitl86w2Imbt904rbfOsO2SK0NOBuoLRiNt96A2Lmbt+04jbfukO2CC0NuBsorZjNt96AmLnbN624zbfukC1CSwPuBkorZvOtNyBm7vZNK27zrTtki9DSgLuB0orZfOsNiJm7fdOK23zrDtkitDTgbqC0YjbfegNi5m7ftOI237pDtggtDbgbKK2YzbfegJi52zetuM237pAtQksD7gZKK2bzrTcgZu72TStu8607ZIvQ0oC7gdKK2XzrDYiZu33Titt86w7ZIrQ0MPPxsT/URStO0/rxrTcgZtSd4jdqz9QgtDQw68axP+FOK06bdcMs73oDYkbdKX6j9kwNQksDc7enP7FOK2abe/pc73oDYkbdKX6j9kwNQksjrQvM7F3Vn3SnFafNvm62WdDiWWdA7Kg7hW7UnqlDaJmISgFRqlZ3IMeap7Zp+Ws9JJ9yKuvFu76A6YC6U6hG7SkGQgsAAIgCoQUAAESB0AIAAKJAaAEAAFEgtAAAgCgQWgAAQBQILQAAIAqEFgAAEAVCCwAAiAKhBQAARIHQAgAAokBoAQAAUSC0AACAKBBaAABAFAgtAAAgCoQWAAAQBUILAACIAqEFAABEgdACAACiQGgBAABRILQAAIAoEFoAAEAUCC0AACAKhBYAABAFQgsAAIgCoQUAAESB0AIAAKJAaAEAAFEgtAAAgCgQWgAAQBQILQAAIAqEFgAAEAVCCwAAiAKhBQAARIHQAgAAokBoAQAAUSC0AACAKBBaAABAFAgtAAAgCoQWAAAQBUILAACIAqEFAABEgdACAAAisMD8F2vThlHi9ugQAAAAAElFTkSuQmCC
