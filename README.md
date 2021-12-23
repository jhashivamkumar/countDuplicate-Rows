# countDuplicate-Rows


if (!this.IsPostBack)
    {
        DataSet ds = new DataSet();
        DataTable dt = new DataTable("Employee");
        dt.Columns.Add(new DataColumn("Id", typeof(string)));
        dt.Columns.Add(new DataColumn("Empname", typeof(string)));
        dt.Columns.Add(new DataColumn("Des", typeof(string)));
        dt.Rows.Add(1, "sk", "eng");
        dt.Rows.Add(2, "rm", "eng");
        dt.Rows.Add(3, "sk", "dt");
        ds.Tables.Add(dt);
 
        Array distinctName;
        for (int i = 0; i < ds.Tables.Count; i++)
        {
            distinctName = ds.Tables[i].AsEnumerable()
                           .GroupBy(x => x.Field<string>("Empname"))
                           .Select(g => new
                           {
                               Name = g.Key,
                               Count = g.Select(x => x.Field<string>("Empname")).Count()
                           }).ToArray();
        }
    }
