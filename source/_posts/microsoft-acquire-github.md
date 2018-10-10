---
title: 마이크로소프트의 깃허브 인수가 개발자에게 희소식인 이유
images: 'images/ms_github.png'
---
## Table of Contents
<!-- toc -->

어제자 기사에 따르면 현지 날짜로 6월 3일 마이크로소프트(MS)가 깃허브를 8조에 인수한다고 발표했습니다. 

많은 개발자 분들이 깃허브를 이용하시고, 이 소식을 깃허브 들어가서 알고 계실텐데요.

요렇게 뜨죠:

![github.com/ahnsv](/images/github.com_ahnsv.png)

아직 인수가 완료된 상황은 아니지만 이번 년도 말 까지 완료한다고 [깃허브피셜](https://blog.github.com/2018-06-04-github-microsoft/)이 떴네요.

## The Dark Side of Github

깃허브는 2700만명 이상의 개발자들의 사실상 표준 플랫폼으로써 350만불 이상 벤처 캐피털 자금으로 펀딩된 기업입니다. 

하지만, 엄청난 유저 베이스와 펀딩에도 불구하고 깃허브는 몇 년간 그럴 듯 성과를 내지 못했는데요. 그와 더불어 깃허브의 가장 중요한 오픈소스 프로젝트들과 개발자들과 소통 문제가 이슈가 되기도 했습니다. 다음은 2016년에 오픈 소스 개발자들로 부터 공개 된 [오픈 레터의 일부 입니다.](https://github.com/dear-github/dear-github) 

> "우리들은 이제 지쳤습니다. 깃허브의 많은 인기 있는 프로젝트를 운영하는 개발자들은 무시당한 기분을 느낍니다. 유일한 서포트 채널을 통해 소통하려했지만, 돌아오는 것은 없었고, 우리들의 요청이 어떻게 되었는지 소식조차 알 수 없었습니다. 우리들의 프로젝트들이 개방적인 환경에서 보통 다뤄지기 떄문에, 가장 중요한 프로젝트 의존성들이 잊혀지는 걸 이해할 수 없습니다."

깃헙 내부적인 문제도 많았습니다. 그 중 대중에게 공개된 이슈들 중 하나로는 2014년에 Julie Ann Horvath가 깃허브의 기업 문화가 성차별적이고 그녀가 깃허브에서 나오는 과정에서 느꼈던 위협들에 대해 이야기하므로써 세계 최대의 개발자 커뮤니티라는 겉모습에 가려진 [그늘을 드러냈습니다](https://techcrunch.com/2014/03/15/julie-ann-horvath-describes-sexism-and-intimidation-behind-her-github-exit/). 이를 개선하기 위해 깃허브의 공동 창업자 Chris Wanstrath는 기업 문화를 변화시키기 위해 [부단한 노력](http://uk.businessinsider.com/github-the-full-inside-story-2016-2?international=true&r=UK&IR=T)을 했습니다. 타 기업들과의 관계도 개선하기 위해 만든, 기업들의 소프트웨어들을 위한 플랫폼, [Github Enterprise](https://enterprise.github.com/home)는 그 일환으로 꽤 좋은 평가를 받았습니다.

이런 내부적인 문제들을 해결하기 위해 깃허브는 많은 노력을 했지만, 지난 7개월 간 CEO가 없이 운영되어 오는 등 여전히 해결되지 않은 기업 내부적인 문제들이 남아있었습니다. 결국, 마이크로소프트에 인수가 되었습니다.

## Why MS?

마이크로소프트는 깃허브의 최다 오픈소스 컨트리뷰터입니다. 프로젝트의 공유 수로 보나, 스타 수로 보나 다른 기업들은 쨉(?)도 안되는 압도적인 1위입니다. 깃허브의 Electron 기반 코드 에디터, [VSCode](https://code.visualstudio.com/), 자바스크립트로 컴파일 되는, 자바스크립트 타입의 상위 집합, [TypeScript](https://github.com/Microsoft/TypeScript), 오픈소스 [.Net Framework](https://github.com/Microsoft/dotnet), 윈도우 OS에서 구동가능한 UNIX Shell, [WSL](https://github.com/Microsoft/WSL) 등이 있죠. 모두 개발자 커뮤니티에서 유명한 프로젝트들이라 많은 분들이 익히 들어보셨을 듯 합니다. 

그동안 MS는 부정적인 이미지가 강했습니다. 많은 IT 업체들을 인수하고, 상업화하고 말아먹었죠(?). 잘 돌아가는 사업을 인수해서 완전 마소화 시키곤 기존의 유저들이 대부분 떠나갔습니다. 또한 오픈 소스 프로젝트들에 대해 부정적인 시각을 가지고 있었습니다. 예를 들면 리눅스라던가... 리눅스라던가...

그래서 몇몇 사람들은 마이크로소프트의 깃허브 인수를 좋지 않은 시각으로 보고 있습니다. 오픈 소스의 죽음이다 라면서요. 하지만, 깃허브가 이런 제스쳐를 취한 가장 큰 이유 중 하나는 2014년 CEO로 부임한 Satya Nadella라고 합니다. 위에 언급한 것과 같은 MS의 많은 오픈 소스 프로젝트들과 코드 개발 폐쇄성을 없앤 데에 강한 인상을 받았다고 [전했습니다](https://www.theverge.com/2018/6/3/17422752/microsoft-github-acquisition-rumors).

개인적으로 또한 기대되는 이유가 MS의 LinkedIn인수 때문입니다. 많은 기존의 유저가 LinkedIn이 MS에 인수된지도 모를 만큼 기존의 시스템을 유지하고 기존의 아이덴티티를 지켜주는 정책을 취하고 있습니다. 또한 Satya Nadella는 [마이크로소프트 블로그](https://blogs.microsoft.com/blog/2018/06/04/microsoft-github-empowering-developers/)에 다음과 같이 밝혔습니다. 

> 무엇보다도, 깃허브의 비전은 우리의 비전과 잘 들어 맞습니다. 우리는 모두 깃허브가 모든 개발자들을 위한 열린 플랫폼으로 남아야한다고 믿습니다. 어떤 언어나 스택, 플랫폼, 클라우드, 라이센스를 사용하든 깃허브는 계속해서 여러분들의 Home일 것입니다 -- 최고의 소프트웨어 개발, 협업, 그리고 발견의 장으로써 말이죠. 

때문에 MS의 인수가 개발자 최대 커뮤니티로서의 깃허브의 아이덴티티를 해칠 거라고 생각되지 않습니다. 오히려 더 좋은 DR(Developer Relations)을 가진 기업으로 성장할 것이라고 생각합니다.

**여러분들은 어떻게 생각하십니까?** 

참고한 문서

* [MS Blog - Microsoft + GitHub = Empowering Developers by Satya Nadelia](https://blogs.microsoft.com/blog/2018/06/04/microsoft-github-empowering-developers/)
* [Github Blog - A bright future for GitHub by @defunkt](https://blog.github.com/2018-06-04-github-microsoft/)
* [zdnet - 마이크로소프트, 깃허브 인수한다 by 이정현 기자](http://www.zdnet.co.kr/news/news_view.asp?artice_id=20180604084605)
* [TechCrunch - Julie Ann Horvath Describes Sexism And Intimidation Behind Her GitHub Exit by Alex Wilheim](https://techcrunch.com/2014/03/15/julie-ann-horvath-describes-sexism-and-intimidation-behind-her-github-exit/)
* [보안 뉴스 - MS가 깃허브를 인수했는데, IT 업계가 왜 시끄러울까? by 문가용 기자](http://www.boannews.com/media/view.asp?idx=70101&utm_source=gaerae.com&utm_campaign=%B0%B3%B9%DF%C0%DA%BD%BA%B7%B4%B4%D9&utm_medium=social)
* [Medium - Microsoft acquiring GitHub is a good thing. Here’s why.
 by Own Williams](https://medium.com/@ow/microsoft-acquiring-github-is-a-good-thing-heres-why-6a6a57eb83ac)