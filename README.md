# exportExcel
调用后端接口,导出excel

#### 导出excel表格
```
        exportExcel() {
            let params = this.searchData;
            params.page = -1;
            exportCardsInfo(params)
            .then( res => {
                if (res.data.type == 'application/json') {
                  this.$message.error('导出提示！', '当前未查询到数据，请核查查询条件！');
                  return;
                }
                var blob = new Blob([res.data], {type: "application/vnd.ms-excel"});
                var fileName = "账号名片列表";
                var a = document.createElement("a");
                document.body.appendChild(a);
                a.download = fileName;
                a.href = URL.createObjectURL(blob);
                a.addEventListener("click", function (evt) {
                  evt.stopPropagation();
                });
                a.click();
            })
            .catch( err => {

            })
        },

```
#### axios请求配置
```
export const exportCardsInfo = params => {
    return axios({
        method: 'post',
        url: '/userManager/exportCardsInfo',
        data: params,
        responseType: 'blob'
    })
}
```
