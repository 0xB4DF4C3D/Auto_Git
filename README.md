# �ϴ� ��
---
���콺 ������ �޴��� `���� ������ Github�� ����` ��� �߰�.


# ����
---
git�� ������� �ʴ� ȯ�濡�� git�� ����ϰ� �Ǹ� ������ ������Ʈ���� git repository�� �����ϰ� remote ������ �����ϰ� add�ϰ� commit�ϰ� remote add ... ���� ����� �ʿ��߽��ϴ�. git�� �ƿ� ó������ ���ٸ� �Ź� �� �� ���� �׷��� �ص� ������ �ʰ����� ������ �ٸ� ������Ʈ ���ʰ��� ��� �̷��� �ϱ�� ������ ������.


�׷��� ���콺 �����ʿ� ���� ������ �ڵ����� GitHub�� �����ϴ� ����� �߰��ϸ� ���Ұ� ���ҽ��ϴ�. ���� ������ GitHub GUI������ Ŭ�� ������� GitHub�� �������� ���ִµ���. ( ������ �� �����ϱ���� �մϴ�. ) �׷����� �ұ��ϰ� �� ����� ������ ���� ����鿡�� ��õ�˴ϴ�.

1. ��� ������ ������ �����
<br /> -> ���ϴ� ��ο��� ���콺 �����ʸ� ������ �˴ϴ�.

2. Publish �����⵵ ������ �����
<br /> -> ...
	
3. ������ ������� �����ϱ� �� ��������� �𸣰ڳ׿�. �׷��� �� ������ ������;
<br />-> ���� ���������� ���� �����ߴ� �ڷ���� Git �ڵ������� �߰��� �� ���� �ֽ��ϴ�.

# ����
---
1. GitAuto.reg�� �����Ų��.
2. C:\gitignores\base.ignore��� �̸��� ������ ���� �⺻���� ������ .gitignore ������ ���´�.
3. IE�� github�� �ڵ��α����� �صд�.
4. ��

# �۵�����
---
�ƹ����� ������Ʈ���� �����ϰ� ��Ʈ��ũ�� �����ϴ� �� ����½�� �ൿ�� ���� �ϹǷ� �� �� �ȵǴ� �ڵ带 ���� �帮�� ������ ������

    [void][Reflection.Assembly]::LoadWithPartialName('Microsoft.VisualBasic'); 
     -> Repository �̸��� �ޱ����� Prompt�� �����ؾ� �ϹǷ� VisualBasic ������� �ε��մϴ�.

    $newRepositoryName = [Microsoft.VisualBasic.Interaction]::InputBox('Repository name', 'Plz input');
    -> ���� ������ Repository �̸��� �޽��ϴ�.

    $ie = New-Object -com internetexplorer.application; 
    -> ���ο� IE ��ü�� �����մϴ�.

    $ie.navigate('https://github.com/new');
    -> https://github.com/new�� �̵��մϴ�. �� �� IE�� �ڵ��α����� �Ǿ��־�� �մϴ�.

    while ($ie.busy -eq $true){ Start-Sleep 1; }; 
    -> �ε� �� �� ���� ��ٸ��ϴ�.

    $formName = $ie.Document.getElementsByName('repository[name]'); 
    @($formName)[0].value = $newRepositoryName; 
    $submitButton = ($ie.document.getElementsByTagName('button') | ? {$_.textContent -like '*Create*'}); 
    $submitButton.click(); 
    -> �Ʊ� ���� Repository �̸����� ���ο� Repository ����

    $newURL = $ie.LocationURL; 
    cd %cd%; 
    git remote add origin $newURL; 
    git push origin master; 
    ->���� ������ �� github repository�� push �մϴ�.

    $ie.Refresh(); 
    $ie.visible = $true;
    -> push�� ��� ������ ���� ������� github �������� �����ݴϴ�.

�������� �ڵ�� �����ϴ�.

# �׷��� ���Դϴ�
---
�� �ڵ忡�� �ǵ�ġ �ʰ� ���� ���͸� ������ �� �� �ֽ��ϴ�. �� �� �����ϼ���. ������ �ظ��ϸ� �����Ŷ� �����մϴ�. ã���ø� �˷��ּ���. 

�� �׸��� �̰� �������� 7, .NET Framework 4.0 ������ ������ Ȯ�εǾ����ϴ�. ������ ����ٸ� �˷��ֽø� �����ϰڽ��ϴ�.

�� �׸��� ��� git�� �ẻ�� �����ϵ� �ȵǼ� ����Ŷ� ���� �Ǽ��Ѱ� ���� ���� �ֽ��ϴ�. Ȥ�� ã���ø� �˷��ּ���.

�̵��� ������� �о��ּż� �����մϴ�.

# �鹮�� �ҿ��ϰ�
---

![���콺 ������ �޴�](https://github.com/0xB4DF4C3D/Auto_Git/imgs/1.png "���콺 ������ �޴�")

![Repository �̸�](https://github.com/0xB4DF4C3D/Auto_Git/imgs/2.png "Repository �̸�")

![���](https://github.com/0xB4DF4C3D/Auto_Git/imgs/3.png "���")