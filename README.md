# asset-portfolio

data=importdata('C:\Users\doubaoer\Desktop\asset management\assignment1\Return.xlsx');
spxtdata=data.data(:,1:2);
spxtdata(:,1)=x2mdate(spxtdata(:,1));
%annualized return
longr=cumprod(spxtdata(:,2)+1);
tomos=size(spxtdata(:,2));
anret=longr(end)^(12/tomos(:,1))-1;

%annualized volatility
anvol=sqrt(12)*std(spxtdata(:,2));

%return to risk ratio
RRT=anret/anvol;

%maximum drawdown:A maximum drawdown (MDD) is the maximum loss from a peak 
% to a trough of a portfolio, before a new peak is attained.(最大回撤）
MDD=maxdrawdown(longr);

%maximum 1-year loss
fre=tomos(1,1)-11;
rollr=zeros(fre,1);
for i=1:fre
   year1=cumprod(spxtdata(i:i+11,2)+1);
  rollr(i)=year1(end)-1;
end
maxloss=min(rollr);



