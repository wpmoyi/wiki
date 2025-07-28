[[_Toc_]]
# lwext4 文件操作接口
```
static const struct dfs_file_ops _extfs_fops =
{
    .open       = dfs_ext_open,
    .close      = dfs_ext_close,
    .ioctl      = dfs_ext_ioctl,
    .read       = dfs_ext_read,
    .write      = dfs_ext_write,
    .flush      = dfs_ext_flush,
    .lseek      = dfs_ext_lseek,
    .truncate   = dfs_ext_truncate,
    .getdents   = dfs_ext_getdents,
};
```