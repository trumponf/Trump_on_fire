# Trump_on_fire
import React, { useEffect, useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { PieChart, Pie, Cell, Tooltip, Legend } from "recharts";

const mockData = {
  name: "Trump on Fire",
  symbol: "TRUF",
  totalSupply: 1000000,
  ownerWallet: "0xYourWalletAddress",
  ownerShare: 150000,
};

export default function TrufDashboard() {
  const [data, setData] = useState(mockData);

  const distribution = [
    { name: "Your Wallet", value: data.ownerShare },
    { name: "Public Supply", value: data.totalSupply - data.ownerShare },
  ];

  const COLORS = ["#FF8042", "#0088FE"];

  return (
    <div className="p-6 max-w-4xl mx-auto">
      <h1 className="text-3xl font-bold mb-4 text-center">{data.name} ({data.symbol}) Dashboard</h1>
      <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
        <Card>
          <CardContent>
            <h2 className="text-xl font-semibold mb-2">Token Info</h2>
            <p><strong>Name:</strong> {data.name}</p>
            <p><strong>Symbol:</strong> {data.symbol}</p>
            <p><strong>Total Supply:</strong> {data.totalSupply.toLocaleString()} TRUF</p>
            <p><strong>Owner Wallet:</strong> {data.ownerWallet}</p>
            <p><strong>Owner Share:</strong> {data.ownerShare.toLocaleString()} TRUF (15%)</p>
          </CardContent>
        </Card>

        <Card>
          <CardContent>
            <h2 className="text-xl font-semibold mb-2">Token Distribution</h2>
            <PieChart width={300} height={250}>
              <Pie
                data={distribution}
                cx="50%"
                cy="50%"
                labelLine={false}
                label={({ name, percent }) => `${name} ${(percent * 100).toFixed(0)}%`}
                outerRadius={80}
                fill="#8884d8"
                dataKey="value"
              >
                {distribution.map((entry, index) => (
                  <Cell key={`cell-${index}`} fill={COLORS[index % COLORS.length]} />
                ))}
              </Pie>
              <Tooltip />
              <Legend />
            </PieChart>
          </CardContent>
        </Card>
      </div>
    </div>
  );
}
