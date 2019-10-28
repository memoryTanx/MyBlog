- `easy_install`

- 查看 pip 版本及路径 `pip -V`
- 更新 pip `pip python -m pip install --upgrade pip`
- 查询所有已安装的包 `pip list`
- 查询可升级的包 `pip list --outdate`
- 安装包 `pip install xxx`
- 卸载包 `pip uninstall xxx`
- 安装指定版本的包 `pip install xxx==2.0`
- 强制更新xxx库 `pip install --ignore-installed xxx`

- 将已安装的包导出 `pip freeze >  ./requirements.txt`
- 导入 `pip install -r requirements.txt`
