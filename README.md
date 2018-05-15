## 个人博客

—— 基于django1.10以及bootstrap3.0

----------
### 简介
> 目前博客功能拥有基本的分页、评论、详细阅读的功能
按标题搜索的功能

>今天对博客的页面以及代码进行了优化，同时，添加了阅读量随点击增加的功能
```python
class ArticleDetailView(DetailView):
	......
 # 从数据库中获取id为pk_url_kwargs的对象
    def get_object(self, queryset=None):
        obj = super(ArticleDetailView, self).get_object()
        # 点击一次阅读量增加一次
        obj.views += 1
        obj.save()
        obj.body = markdown.markdown(obj.body, safe_mode='escape',
        extensions=[
            'markdown.extensions.nl2br',
            'markdown.extensions.fenced_code'
        ])
        return obj
	......
```
**安装**
- 首先需要安装相关数据库，我这里用mysql做示范(鉴于大家的普遍使用), [ubuntu安装参考][7], 然后创建一个名为blog的数据库
- (可选)redis 安装， [安装参考][8]，然后启动redis
- 新建一个虚拟环境，然后安装相关模块```pip install -r requirements/dev.txt```
- 初始化表```python manage.py migrate```
- 最后运行```python manage.py runserver```

--------
