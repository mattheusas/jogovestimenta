# jogovestimentaimport Link from "next/link";
import { Button } from "@/components/ui/button";
import { Card, CardContent, CardFooter, CardHeader, CardTitle } from "@/components/ui/card";
import { useState } from "react";

const outfits = [
  { id: 1, name: "Terno e Gravata", category: "formal", image: "/images/terno_gravata.png" },
  { id: 2, name: "Camisa Social e Calça", category: "formal", image: "/images/camisa_social.png" },
  { id: 3, name: "Camiseta e Jeans", category: "casual", image: "/images/camiseta_jeans.png" },
  { id: 4, name: "Roupa Esportiva", category: "inadequado", image: "/images/roupa_esportiva.png" },
  { id: 5, name: "Vestido Formal", category: "formal", image: "/images/vestido_formal.png" },
  { id: 6, name: "Jaqueta de Couro", category: "criativo", image: "/images/jaqueta_couro.png" },
  { id: 7, name: "Bermuda e Chinelo", category: "inadequado", image: "/images/bermuda_chinelo.png" },
];

export default function InterviewLookGame() {
  const [selectedOutfit, setSelectedOutfit] = useState(null);
  const [feedback, setFeedback] = useState("");

  const handleSelect = (outfit) => {
    setSelectedOutfit(outfit);
  };

  const handleEvaluate = () => {
    if (!selectedOutfit) {
      setFeedback("Escolha uma roupa antes de avaliar!");
      return;
    }

    if (selectedOutfit.category === "formal") {
      setFeedback("Ótima escolha! Você está pronto para a entrevista.");
    } else if (selectedOutfit.category === "inadequado") {
      setFeedback("Essa roupa não é adequada para entrevistas!");
    } else {
      setFeedback("Essa roupa pode até servir, mas há opções melhores!");
    }
  };

  return (
    <div className="flex flex-col items-center p-6">
      <h1 className="text-2xl font-bold mb-4">Escolha a Vestimenta para a Entrevista</h1>
      <div className="grid grid-cols-2 gap-4">
        {outfits.map((item) => (
          <Card
            key={item.id}
            className={`cursor-pointer p-4 border ${
              selectedOutfit?.id === item.id ? "border-blue-500" : ""
            }`}
            onClick={() => handleSelect(item)}
          >
            <CardContent>
              <img src={item.image} alt={item.name} className="w-full h-40 object-cover" />
              <p className="text-center mt-2">{item.name}</p>
            </CardContent>
          </Card>
        ))}
      </div>
      <Button className="mt-4" onClick={handleEvaluate}>Avaliar Escolha</Button>
      {feedback && <p className="mt-2 text-lg font-semibold">{feedback}</p>}
    </div>
  );
}
