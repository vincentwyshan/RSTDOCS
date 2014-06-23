启动sentry
===========
#. 安装 `sudo easy_install -UZ sentry`
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
