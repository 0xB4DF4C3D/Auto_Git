# 하는 일
---
마우스 오른쪽 메뉴에 `현재 폴더를 Github과 연동` 기능 추가.


# 목적
---
git을 사용하지 않던 환경에서 git을 사용하게 되면 기존의 프로젝트들을 git repository로 설정하고 remote 서버를 설정하고 add하고 commit하고 remote add ... 등의 노력이 필요했습니다. git을 아예 처음부터 쓴다면 매번 할 때 마다 그렇게 해도 귀찮지 않겠지만 성격이 다른 프로젝트 수십개를 모두 이렇게 하기란 귀찮은 일이죠.


그래서 마우스 오른쪽에 현재 폴더를 자동으로 GitHub과 연동하는 기능을 추가하면 편할것 같았습니다. 물론 기존의 GitHub GUI에서도 클릭 몇번으로 GitHub과 연동까지 해주는데요. ( 심지어 더 안전하기까지 합니다. ) 그럼에도 불구하고 이 기능은 다음과 같은 사람들에게 추천됩니다.

1. 경로 지정도 귀찮은 사람들
<br /> -> 원하는 경로에서 마우스 오른쪽만 누르면 됩니다.

2. Publish 누르기도 귀찮은 사람들
<br /> -> ...
	
3. 솔직히 여기까지 쓰고나니까 왜 만들었는지 모르겠네요. 그래도 뭐 쓰려면 쓰세요;
<br />-> 저는 개인적으로 과거 공부했던 자료들을 Git 자동관리에 추가할 때 쓰고 있습니다.

# 사용법
---
1. GitAuto.reg을 실행시킨다.
2. C:\gitignores\base.ignore라는 이름의 파일을 만들어서 기본으로 적용할 .gitignore 내용을 적는다.
3. IE로 github에 자동로그인을 해둔다.
4. 끝

# 작동원리
---
아무래도 레지스트리를 수정하고 네트워크에 접속하는 등 수상쩍은 행동을 많이 하므로 몇 줄 안되는 코드를 설명 드리면 다음과 같으며

    [void][Reflection.Assembly]::LoadWithPartialName('Microsoft.VisualBasic'); 
     -> Repository 이름을 받기위해 Prompt를 생성해야 하므로 VisualBasic 어셈블리를 로드합니다.

    $newRepositoryName = [Microsoft.VisualBasic.Interaction]::InputBox('Repository name', 'Plz input');
    -> 새로 생성할 Repository 이름을 받습니다.

    $ie = New-Object -com internetexplorer.application; 
    -> 새로운 IE 객체를 생성합니다.

    $ie.navigate('https://github.com/new');
    -> https://github.com/new로 이동합니다. 이 때 IE에 자동로그인이 되어있어야 합니다.

    while ($ie.busy -eq $true){ Start-Sleep 1; }; 
    -> 로드 될 때 까지 기다립니다.

    $formName = $ie.Document.getElementsByName('repository[name]'); 
    @($formName)[0].value = $newRepositoryName; 
    $submitButton = ($ie.document.getElementsByTagName('button') | ? {$_.textContent -like '*Create*'}); 
    $submitButton.click(); 
    -> 아까 받은 Repository 이름으로 새로운 Repository 생성

    $newURL = $ie.LocationURL; 
    cd %cd%; 
    git remote add origin $newURL; 
    git push origin master; 
    ->현재 폴더를 새 github repository에 push 합니다.

    $ie.Refresh(); 
    $ie.visible = $true;
    -> push가 모두 끝나면 새로 만들어진 github 페이지를 보여줍니다.

악의적인 코드는 없습니다.

# 그런데 말입니다
---
이 코드에서 의도치 않게 공격 벡터를 제공해 줄 수 있습니다. 그 점 주의하세요. 하지만 왠만하면 없을거라 생각합니다. 찾으시면 알려주세요. 

아 그리고 이건 윈도우즈 7, .NET Framework 4.0 에서만 구동이 확인되었습니다. 문제가 생긴다면 알려주시면 감사하겠습니다.

아 그리고 사실 git을 써본지 일주일도 안되서 만든거라 제가 실수한게 있을 수도 있습니다. 혹시 찾으시면 알려주세요.

이딴걸 여기까지 읽어주셔서 감사합니다.

# 백문이 불여일견
---

![마우스 오른쪽 메뉴](https://github.com/0xB4DF4C3D/Auto_Git/imgs/1.png "마우스 오른쪽 메뉴")

![Repository 이름](https://github.com/0xB4DF4C3D/Auto_Git/imgs/2.png "Repository 이름")

![결과](https://github.com/0xB4DF4C3D/Auto_Git/imgs/3.png "결과")