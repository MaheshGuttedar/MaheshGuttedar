@{
      ViewBag.Title = "User List";
      Layout = "~/Views/Shared/_Layout.cshtml";
}
@section ScriptsOrCss
{
    
    <link href="~/Content/DataTable/new/dataTables.bootstrap.css" rel="stylesheet" type="text/css"/> 
    <script src="~/Content/DataTable/new/jquery.dataTables.min.js" type="text/javascript"></script>
    <script src="~/Content/DataTable/new/dataTables.buttons.min.js" type="text/javascript"></script>
    <script src="~/Content/DataTable/new/jszip.min.js" type="text/javascript"></script>
    <script src="~/Content/DataTable/new/pdfmake.min.js" type="text/javascript"></script>
    <script src="~/Content/DataTable/new/vfs_fonts.js" type="text/javascript"></script>
    <script src="~/Content/DataTable/new/buttons.html5.min.js" type="text/javascript"></script>
    <link href="~/Content/DataTable/new/jquery.dataTables.min.css" rel="stylesheet" type="text/css"/>
    <link href="~/Content/DataTable/new/buttons.dataTables.min.css" rel="stylesheet" type="text/css"/>
    <script src="~/Content/DataTable/new/buttons.print.min.js"></script>
    <script src="~/Content/DataTable/new/buttons.colVis.min.js"></script> 
}
    <section class="content-header">
        <h1>
            @ViewBag.Title
            
        </h1>
    </section>

    <section class="content">
        <!-- Small boxes (Stat box) -->
        <div class="row">
            <div class="col-xs-12">
                <div class="box box-solid box-primary">

                    <div class="box-body">
                        <!-- Split button -->
                        <div class="margin"> 
                            <div class="btn-group"> 
                                @Ajax.ModalDialogActionLink("Create Quick", "Create", "Create ", "btn btn-dropbox") 
                            </div> 
                            <div class="btn-group"> 
                                <a href="~/User/Create" class="btn btn-default">Create Full</a>
                            </div>  
                        </div>
                        <!-- flat split buttons -->
                    </div><!-- /.box-body -->
                </div>
                <div class="box box-solid box-primary">
                    <div class="box-header">
                        <h3 class="box-title">@ViewBag.Title</h3>
                    </div><!-- /.box-header -->
                    <div class="box-body table-responsive">

                        <div class="margin">

                            <div class="streaming-table">
                                <span id="found" class="label label-info"></span>


                                <table id="tbUser" class="display nowrap">
                                    <thead>
                                        <tr>
                                            <th>Actions</th>
                                            <th> Id  </th>
                                            <th> Username  </th>
                                            <th> Password  </th>

 
                                        </tr>
                                    </thead>
                                    <tbody></tbody>
                                </table>

                                <div id="summary">
                                    <div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="box box-solid box-primary">

                    <div class="box-body">
                        <!-- Split button -->
                        <div class="margin">
                            <div class="btn-group"> 
                                @Ajax.ModalDialogActionLink("Create Quick", "Create", "Create ", "btn btn-dropbox") 
                            </div> 
                            <div class="btn-group"> 
                                <a href="~/User/Create" class="btn btn-default">Create Full</a>
                            </div> 
                        </div>
                        <!-- flat split buttons -->
                    </div><!-- /.box-body -->
                </div>
            </div>
        </div>
    </section>





     <script type="text/javascript">

        $(document).ready(function () {
            var oTableUser = "";
            var ControlerNameUser = "@Url.Content("~/User")";
            // debugger;
            oTableUser = $("#tbUser").dataTable({  
            "bRetrieve": true,
            "bProcessing": true,
            "dom": 'lBfrtip',
            "sAjaxSource": "@Url.Content("~/User/GetGrid")",
            "buttons": [
                 { extend: 'copyHtml5', exportOptions: { columns: ':visible' } }
                ,{ extend: 'excelHtml5', exportOptions: { columns: ':visible' } }
                ,{ extend: 'csvHtml5', exportOptions: { columns: ':visible' } }
                ,{ extend: 'pdfHtml5', exportOptions: { columns: ':visible' } }
                ,{ extend: 'print', exportOptions: { columns: ':visible' } } 
                ,'colvis'
            ], columnDefs: [{   visible: false }],
            "pageLength": 10,
            "lengthMenu": [[5,10, 25, 50, -1], [5,10, 25, 50, "All"]],
                "aoColumns": [
                             
                {
                                 "mRender": function (oObj, type, row) {
                                     
 var buttons = '<div class="text-center"> <div class="btn-group text-left"> <button type="button" class="btn btn-default btn-xs btn-warning dropdown-toggle" data-toggle="dropdown">Action <span class="caret"></span></button>';
                    buttons += '<ul class="dropdown-menu pull-left" role="menu">';
                    buttons += '<li><a href="' + ControlerNameUser + "/MultiViewIndex/" + row[0] + '"><i class="fa fa-edit"></i>Full Edit</a></li>';
                    buttons += '<li class="divider"></li>';
                    buttons += '<li><a href="' + ControlerNameUser + "/Edit/" + row[0] + '" data-ajax-update="#SkEdit" data-ajax-success="openModalDialog(\'SkEdit\', \'Edit\')" data-ajax-mode="replace" data-ajax-method="GET" data-ajax-failure="clearModalDialog(\'SkEdit\');alert(\'Ajax call failed\')" data-ajax-begin="prepareModalDialog(\'SkEdit\')" data-ajax="true"><i class="fa fa-pencil-square"></i>Quick Edit</a></li>';
                    buttons += '<li><a href="' + ControlerNameUser + "/Details/" + row[0] + '" data-ajax-update="#SkDetails" data-ajax-success="openModalDialog(\'SkDetails\', \'Details\')" data-ajax-mode="replace" data-ajax-method="GET" data-ajax-failure="clearModalDialog(\'SkDetails\');alert(\'Ajax call failed\')" data-ajax-begin="prepareModalDialog(\'SkDetails\')" data-ajax="true"><i class="fa fa-info-circle"></i>Quick Details</a></li>';
                    buttons += '<li><a href="' + ControlerNameUser + "/Delete/" + row[0] + '" data-ajax-update="#SkDelete" data-ajax-success="openModalDialog(\'SkDelete\', \'Delete\')" data-ajax-mode="replace" data-ajax-method="GET" data-ajax-failure="clearModalDialog(\'SkDelete\');alert(\'Ajax call failed\')" data-ajax-begin="prepareModalDialog(\'SkDelete\')" data-ajax="true"><i class="fa fa-trash-o"></i> Delete</a></a></li>';
                     
                    buttons += '</ul>';
                    buttons += '</div></div>';
                    return buttons;
                                 } 
                
        } ,{}
,{}
,{}


        ]

        });
        
        });
    </script>

