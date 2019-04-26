 const columns =[
      {
        key:'1',
        title: '项目名称',
        dataIndex: 'name',
        width: '20%',
        ...this.getColumnSearchProps('name'),
      }, {
        key:'2',
        title: '描述',
        dataIndex: 'description',
        width: '20%'
      }, {
        key:'3',
        title: '创建时间',
        dataIndex: 'creation_timestamp',
        render: (data) =>{
          var d = new Date(data);
          var times= d.getFullYear() + '-' + (d.getMonth() + 1) + '-' + d.getDate() + ' ' + d.getHours() + ':' + d.getMinutes() + ':' + d.getSeconds();
          return times
        }
      },{
        key:'4',
        title: '状态',
        dataIndex: 'status',
        render: (text,record) => {

          return (
            <div>
              {
                 (() => {
                      switch (record.status) {
                        case 'Active':
                          return <Tag color="green">{record.status} </Tag>;
                        case 'Initial':
                          return <Tag color="blue">{record.status}</Tag>;
                        case 'Terminating':
                          return <Tag color="red">red</Tag>;
                        default:
                          return null;
                    }
                    })()


                }


                {/* {status.map(tag => {
                  let color = tag.length > 5 ? 'geekblue' : 'green';
                  if (tag === 'loser') {
                    color = 'volcano';
                  }
                  return <Tag color={color} key={tag}>{tag.toUpperCase()}</Tag>;
                })} */}
                  
                
            </div>
          )
          },
      },{
       
        title: '操作', dataIndex: 'operator', key: '5', 
        render: (text, record) => (
            <div>
              {
                <div>
                <Button type='default' onClick={()=>this.View(record)}>查看</Button> 
                <Divider type="vertical" /> 
                <Button type='default' onClick={() => this.modify(record) }> 
                     {/* <Link to={{path:'/layout/environment/modify', query: {dotData: record}}}> 修改 </Link> */}
                       {/* <Link to='/layout/environment/modify'>修改</Link> */}
                        修改
                </Button> 
                <Divider type="vertical" />
                <Button type='default' onClick={() => this.handleOk(record)}>发布</Button> 
                    <Modal
                        title="是否发布"
                        visible={this.state.visible}
                        onOk={this.handleOk}
                        onCancel={this.handleCancel}
                        footer={[
                          <Button key="back" onClick={this.handleCancel}>取消</Button>,
                          <Button key="submit" type="primary"  onClick={this.handleOk}>
                            确定
                          </Button>,
                        ]}
                      >
                        <p>是否发布</p>
                        
                      </Modal>
                </div>
              }
            </div>
          )


      }];
      