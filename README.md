import React, { useState } from "react";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";
import { motion } from "framer-motion";

const factories = [
  { name: "مصنع الزيوت العالمية", location: "السعودية", ownerLanguage: "عربي", product: "زيت قلي" },
  { name: "شركة الزيوت الطبيعية", location: "مصر", ownerLanguage: "عربي", product: "زيت زيتون" },
  { name: "Oil King Factory", location: "تركيا", ownerLanguage: "إنجليزي", product: "زيت دوار الشمس" },
];

export default function Home() {
  const [search, setSearch] = useState("");
  const [filteredFactories, setFilteredFactories] = useState([]);

  const handleSearch = () => {
    const results = factories.filter((factory) =>
      factory.product.includes(search) || factory.name.includes(search)
    );
    setFilteredFactories(results);
  };

  return (
    <div className="flex flex-col items-center justify-center min-h-screen bg-gray-100 p-4">
      <motion.h1
        className="text-3xl font-bold mb-6"
        initial={{ opacity: 0, y: -20 }}
        animate={{ opacity: 1, y: 0 }}
      >
        ابحث عن الموردين والمصانع
      </motion.h1>
      <div className="flex gap-2 mb-4">
        <Input
          placeholder="ابحث عن المنتج أو المصنع..."
          value={search}
          onChange={(e) => setSearch(e.target.value)}
        />
        <Button onClick={handleSearch}>بحث</Button>
      </div>
      <div className="grid gap-4 w-full max-w-2xl">
        {filteredFactories.length > 0 ? (
          filteredFactories.map((factory, index) => (
            <Card key={index}>
              <CardContent className="p-4">
                <h2 className="text-xl font-semibold">{factory.name}</h2>
                <p>الموقع: {factory.location}</p>
                <p>لغة المالك: {factory.ownerLanguage}</p>
                <p>المنتج: {factory.product}</p>
              </CardContent>
            </Card>
          ))
        ) : (
          <p className="text-gray-500">لم يتم العثور على نتائج</p>
        )}
      </div>
    </div>
  );
}
