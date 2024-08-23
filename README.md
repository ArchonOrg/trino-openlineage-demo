# openlineage-demo

## quickstart

### Service Up

```sh
# openlineage
git clone https://github.com/MarquezProject/marquez --depth 1 && cd marquez
./docker/up.sh -d

# trino
docker run -d --name trino -v $(pwd)/trino:/etc/trino --network host trinodb/trino
```

### SQL demo

```sql
create table memory."default".cust_order as
select
    t1.orderkey, t1.orderdate, coalesce(t1.totalprice, 1) as totalprice,
    case 
        when t1.orderkey is not null then coalesce(cast(t1.orderkey as varchar), t1.clerk)
        else coalesce(t1.comment, t1.clerk) 
    end as  comment,
    t2.name, t2.phone
from tpch.sf1.orders t1
join tpch.sf1.customer t2
    on t1.custkey = t2.custkey
limit 10;
```

### openlineage web

http://localhost:3000/
