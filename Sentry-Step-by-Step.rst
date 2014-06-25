启动sentry
===========
#. 安装 `sudo easy_install -UZ sentry`
#. `sentry init`
#. `sentry createsuperuser` 创建管理员帐号


启用 Queuing Work
=================
#. 后台运行 `sentry celery worker -B -l WARNING`, 
   在 `~/.sentry/sentry.conf.py` 中启用代码 `CELERY_ALWAYS_EAGER = False`
#. 启用Update Buffers, 反注释 `~/.sentry/sentry.conf.py` 中 `SENTRY_BUFFER = 'sentry.buffer.base.Buffer'`



错误处理
========
- `DatabaseError('database is locked',)` , django数据库backends不要使用sqlite3, 改用其它RDBMS可解决这个问题
- `DatabaseError: (1213, 'Deadlock found when trying to get lock; try restarting transaction')`, 
  通过 `easy_install -UZ sentry` 重新安装问题消失
- 在django runserver启动server时能正常发送exception，在uWSGI模式下不能发送exception，升级django至1.4以上版本能解决该问题
- 在客户端使用 django+raven 发生错误： `No handlers could be found for logger "sentry.errors.client"`， 升级python至2.6.6或者以上版本
