## Qt Network

1. 同步请求数据

   ```c++
   QNetworkAccessManager *mgr = new QNetworkAccessManager(this);
   const QUrl url(QStringLiteral("http://myserver.com/api"));
   QNetworkRequest request(url);
   request.setHeader(QNetworkRequest::ContentTypeHeader, "application/json");
   
   QJsonObject obj;
   obj["key1"] = "value1";
   obj["key2"] = "value2";
   QJsonDocument doc(obj);
   QByteArray data = doc.toJson();
   // or
   // QByteArray data("{\"key1\":\"value1\",\"key2\":\"value2\"}");
   QNetworkReply *reply = mgr->post(request, data);
   
   QObject::connect(reply, &QNetworkReply::finished, [=](){
       if(reply->error() == QNetworkReply::NoError){
           QString contents = QString::fromUtf8(reply->readAll());
           qDebug() << contents;
       }
       else{
           QString err = reply->errorString();
           qDebug() << err;
       }
       reply->deleteLater();
   });
   ```

* TableView 初始化

```c++
void myc::setTableHead()
{
    if(ui->tableView->model()==nullptr){
      QStandardItemModel *  theModel = new QStandardItemModel(ui->tableView);
      ui->tableView->setModel(theModel);
   		 }
    QStandardItemModel * theModel = (QStandardItemModel*) ui->tableView->model();
	 theSelection = new QItemSelectionModel(theModel);//选中模型类 从ui中获取 而不是设置类成员
	 ui->tableView->setSelectionModel(theSelection);
    QStringList headerList;
    headerList<<"序号"<<"报告编号"<<"姓名"<<"性别"<<"创建时间";
    theModel->setHorizontalHeaderLabels(headerList);
    theModel->setRowCount(5);  //设置表格行数 
    ui->tableView->setGridStyle(Qt::SolidLine);
    ui->tableView->horizontalHeader()->setStretchLastSection(true);
    ui->tableView->horizontalHeader()->setSectionResizeMode(QHeaderView::ResizeToContents);
    ui->tableView->verticalHeader()->setVisible(true);   // 是否隐藏列表头
    ui->tableView->setEditTriggers(QAbstractItemView::NoEditTriggers); //是否可编辑 cell
    ui->tableView->setContextMenuPolicy(Qt::CustomContextMenu);    //弹出右键菜单策略
    ui->tableView->setSelectionBehavior(QAbstractItemView::SelectRows); //一选就选择整行
    ui->tableView->setSelectionMode(QAbstractItemView::SingleSelection); //只选择一行/多行
}
```

* 添加一行数据

  ```c++
  void myc::querybtn_clicked()
  {
      
      QStandardItemModel * theModel = (QStandardItemModel*)ui->tableView->model();
      int start= theModel->rowCount();  // 有start也就是从表格现有的行数下一个开始
      QString sql =  QString("select * from patients");
      QList<QList<QVariant>> query_list = con->dbquery(sql);
      for(int i=0;i<query_list.length();i++){
          QList<QStandardItem*> ItemList;
          ItemList<<(new QStandardItem(query_list[i][0].toString()));
          ItemList<<(new QStandardItem(query_list[i][1].toString()));
          ItemList<<(new QStandardItem(query_list[i][2].toString()));
          ItemList<<(new QStandardItem(query_list[i][3].toString()=="0"?"女":"男"));
          ItemList<<(new QStandardItem(query_list[i][4].toString()));
          theModel->insertRow(i+start,ItemList);  // 插入
      }
  
  ```