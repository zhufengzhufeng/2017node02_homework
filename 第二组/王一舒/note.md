#NODE
###brew
https://brew.sh/index_zh-cn.html
brew install git
###����git����˭
git config --list �鿴����
git config --global user.name �û��� 
git config --global user.email ����
###����Ŀ¼
mkdir Ŀ¼����
###cd ����Ŀ¼
cd Ŀ¼��
mkdir test-git && cd test-git
###��ʼ��git�ֿ�
git init ����ʼ����
ls -al �鿴�����ļ� ���������ļ�
###�����ļ�
touch index.txt
###�鿴�ļ�����
cat index.txt
###vi��������
i  ����
esc+ :wq ���沢�Ƴ�
###�鿴git״̬
��ɫ��ʾû�����ݴ�����
��ɫ��ʾ���ݴ�����
git status
###�����ݴ���
git add .
###������ʷ��
git commit -m ''
###�鿴��ʷ
git log --oneline
###git diff
git diff  �ȽϹ��������ݴ���
git diff --cached �ݴ�������ʷ
git diff master ����������ʷ��
###���ݴ����и��ǵ�������
git checkout �ļ���
###ѡ��ĳ���汾���лع�����
git reset --hard �汾id
###�鿴������ʷ�汾
git reflog
###����gitignore������add֮ǰ����
.idea
node_modules
.DS_Store
###ɾ����һ������ݴ���������
git reset HEAD .
###��֧
git branch (�鿴��֧)
git branch ��֧�� (������֧)
###�����ķ�֧��masterһ��
git branch -D ɾ����֧
###�������л�
git checkout -b ��֧�� 
=>
git branch dev
git checkout dev
###�������ύ��ĳ����֧��
Ĭ�����ǵĴ����Ƿ��ڹ������ϣ��������κη�֧��ֻ���ύ��ĳ����֧�ϣ����ļ��Ź������ض��ķ�֧
###fast-forward
����û���κθ���
��֧�ύ���µĴ���
�����ɵ�ָ�����ָ�򵽷�֧���µĴ��뼴��
###�ύ�����ļ�����һ����λ
git commit -a -m 'add hello'
###conflict
�ϲ������֧ʱ���ܺϲ������ݻ������ͻ
�ֶ������ͻ,�ύ���½��
###���������ݵ��ļ�
echo "# 201702nide" > README.md

##�ύ��Զ�ֿ̲�

###�����ļ�
README.md
.gitignore
###�ύ����ʷ��
git add
git commit -m ����Ϣ��
###�鿴Զ�ֿ̲�
git remote -v
git remote add ��ַ�ı��� ��ַ
git push origin master ��master���͵�origin��
###���غ����ϰ汾��һ��
���ϱ����µİ汾��
���Ϻ����������汾����һ��
###��ȡ�����
���������´�����ȡ��master��֧��
git pull origin master ��ȡ���´���
###����git��̬��ҳ
- ����ҳͨ��git��ַ���ʣ�ֻ�ܷž�̬ҳ�����ܷ���server��
###��һ��
- ��Ҫһ���ض��ķ�֧��gh-pages��
git checkout -b gh-pages
- �������ύ�������֧��
git add ```
git commit -m'static'
- �������غ�Զ�̵�����
git remote add ���� ��ַ
- ���͵�github��,��gh-pages�ύ�������֧��
git push origin gh-pages
- ��github�е�setting�Ͽ����ҵ������ַ
###����ϲ���������ύ�ıʼ�

###fork
���ӣ������˵Ĵ��뵱ǰ��״̬����¡һ�ݷŵ��Լ��Ĳֿ��ϣ�һ����Ŀֻ��forkһ�Σ��ҵĴ�����²��ᵼ�������Ŀ����
###clone
��¡�ǽ����ϵ���Ŀ��ȡ�����أ������������git�ֿ⣬�����Ѿ���Ӻ���Զ�ֿ̲��ַ
git clone ��ַ �ļ�������
###�鳤�ύ��Ϣ
git clone �Լ�����Ŀ��ַ
�������
git add .
git commit -m 'team xxx'
git push origin master
###��Ա���ύ���Լ�
git clone �Լ�����Ŀ��ַ
�������
git add .
git commit -m 'team xxx'
git remote add leader �鳤�ĵ�ַ������һ�μ��ɣ�
git pull leader master
git push origin master
###�鳤�ٴ��ύ����ʦ
���Լ������ݷŽ�ȥ
git add .
git commit -m 'team xxx'
git remote add teacher https://github.com/zhufengzhufeng/2017node02_homework
git pull teacher master
git push origin master

##NODE
###���û�������
- node��������������ִ�е�ԭ��
- ����ִ���ļ����õ��˻���������
   - ϵͳ->����->�߼�ϵͳ����->��������->path->��������
###node��ʲô��
���������js�Ļ��������������
###ǰ�˵�ģ�黯��
- �հ�
- ����(����ֻ��һ��): ������ȫ���������ͻ������ʱ�������
- requirejs(AMD)����ǰ�� seajs(CMD)�ͽ�����
commonjs �淶����nodeģ���ʵ�� module.exports
###node�ص�
- �첽io ����ʱ��,�ص�������
- ���߳�(�������Զ��߳�) ���߳�ʵ�־����л�ִ��������(�ٶȺܿ�о��������������ڸɺܶ����)
- �����ǰ����̵߳ģ�nodeһ������ֻ�ܿ�һ���߳�
###�¼���
- ���¼�������
###ȫ�ֶ���
- ǰ�˵�ȫ�ֱ��� ��window �������global
- ȫ�ֶ����ڵ�ǰ�ļ����¿���ֱ��ʹ�õĶ���ȫ�ֶ���
- ȫ�ֶ��� global�ϵ����� + ���������β�
- node��û��window����
```
setTimeout(function () {//��ʱ���е�this �Ƕ�ʱ���Լ�
    console.log(this);
});
~function () {
    console.log(this); //�հ��е�this����global
}();
```