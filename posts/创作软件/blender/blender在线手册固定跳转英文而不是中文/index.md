# Blender在线手册固定跳转英文而不是中文

Blender中文手册某些翻译不准确，英文最符合原意。本文介绍一种跳转在线手册不跟随Blender本身语言的方法。
<!--more-->
打开Blender安装目录文件：
`...\blender-4.2.15-lts.e8cd310002f4\4.2\scripts\modules\bpy\utils\__init__.py`
修改文件：
```Python
def manual_language_code(default="en"):
    """
    :return:
       The language code used for user manual URL component based on the current language user-preference,
       falling back to the ``default`` when unavailable.
    :rtype: str
    """
    # language = _bpy.context.preferences.view.language
    # if language == 'DEFAULT':
    #     language = _os.getenv("LANG", "").split(".")[0]
    language = "en"
    return _manual_language_codes.get(language, default)
```
重启Blender后即可生效。

---

> 作者: [Jason](https://github.com/actforjason)  
> URL: https://actforjason.github.io/posts/%E5%88%9B%E4%BD%9C%E8%BD%AF%E4%BB%B6/blender/blender%E5%9C%A8%E7%BA%BF%E6%89%8B%E5%86%8C%E5%9B%BA%E5%AE%9A%E8%B7%B3%E8%BD%AC%E8%8B%B1%E6%96%87%E8%80%8C%E4%B8%8D%E6%98%AF%E4%B8%AD%E6%96%87/  

